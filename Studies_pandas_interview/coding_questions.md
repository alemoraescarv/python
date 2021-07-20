```python
def async_detect_document(gcs_source_uri, gcs_destination_uri):
    """OCR with PDF/TIFF as source files on GCS"""
    import json
    import re
    from google.cloud import vision
    from google.cloud import storage

    # Supported mime_types are: 'application/pdf' and 'image/tiff'
    mime_type = 'application/pdf'

    # How many pages should be grouped into each json output file.
    batch_size = 2

    client = vision.ImageAnnotatorClient()

    feature = vision.Feature(
        type_=vision.Feature.Type.DOCUMENT_TEXT_DETECTION)

    gcs_source = vision.GcsSource(uri=gcs_source_uri)
    input_config = vision.InputConfig(
        gcs_source=gcs_source, mime_type=mime_type)

    gcs_destination = vision.GcsDestination(uri=gcs_destination_uri)
    output_config = vision.OutputConfig(
        gcs_destination=gcs_destination, batch_size=batch_size)

    async_request = vision.AsyncAnnotateFileRequest(
        features=[feature], input_config=input_config,
        output_config=output_config)

    operation = client.async_batch_annotate_files(
        requests=[async_request])

    print('Waiting for the operation to finish.')
    operation.result(timeout=420)

    # Once the request has completed and the output has been
    # written to GCS, we can list all the output files.
    storage_client = storage.Client()

    match = re.match(r'gs://([^/]+)/(.+)', gcs_destination_uri)
    bucket_name = match.group(1)
    prefix = match.group(2)

    bucket = storage_client.get_bucket(bucket_name)

    # List objects with the given prefix.
    blob_list = list(bucket.list_blobs(prefix=prefix))
    print('Output files:')
    for blob in blob_list:
        print(blob.name)

    # Process the first output file from GCS.
    # Since we specified batch_size=2, the first response contains
    # the first two pages of the input file.
    output = blob_list[0]

    json_string = output.download_as_string()
    response = json.loads(json_string)

    # The actual response for the first page of the input file.
    first_page_response = response['responses'][0]
    annotation = first_page_response['fullTextAnnotation']

    # Here we print the full text from the first page.
    # The response contains more information:
    # annotation/pages/blocks/paragraphs/words/symbols
    # including confidence scores and bounding boxes
    print('Full text:\n')
    print(annotation['text'])
```


```python
async_detect_document('gs://cloud-samples-data/vision/pdf_tiff/census2010.pdf','gs://b2-teste/visionAPI')

```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-26-eb6a61c11713> in <module>()
    ----> 1 async_detect_document('gs://cloud-samples-data/vision/pdf_tiff/census2010.pdf','gs://b2-teste/visionAPI')
    

    <ipython-input-25-c243dda9fc67> in async_detect_document(gcs_source_uri, gcs_destination_uri)
         14     client = vision.ImageAnnotatorClient()
         15 
    ---> 16     feature = vision.Feature(
         17         type_=vision.Feature.Type.DOCUMENT_TEXT_DETECTION)
         18 


    AttributeError: module 'google.cloud.vision' has no attribute 'Feature'



```python
!pip3 install google-cloud-vision
!pip3 install google-cloud-storage
```

    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m
    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m
    Requirement already satisfied: google-cloud-vision in /opt/conda/lib/python3.7/site-packages (2.4.0)
    Requirement already satisfied: packaging>=14.3 in /opt/conda/lib/python3.7/site-packages (from google-cloud-vision) (20.1)
    Requirement already satisfied: proto-plus>=1.15.0 in /opt/conda/lib/python3.7/site-packages (from google-cloud-vision) (1.15.0)
    Requirement already satisfied: google-api-core[grpc]<2.0.0dev,>=1.26.0 in /opt/conda/lib/python3.7/site-packages (from google-cloud-vision) (1.26.1)
    Requirement already satisfied: pytz in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (2019.3)
    Requirement already satisfied: googleapis-common-protos<2.0dev,>=1.6.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (1.51.0)
    Requirement already satisfied: protobuf>=3.12.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (3.12.2)
    Requirement already satisfied: six>=1.13.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (1.14.0)
    Requirement already satisfied: requests<3.0.0dev,>=2.18.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (2.23.0)
    Requirement already satisfied: setuptools>=40.3.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (46.1.1.post20200322)
    Requirement already satisfied: google-auth<2.0dev,>=1.21.1 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (1.27.1)
    Requirement already satisfied: grpcio<2.0dev,>=1.29.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (1.37.0)
    Requirement already satisfied: cachetools<5.0,>=2.0.0 in /opt/conda/lib/python3.7/site-packages (from google-auth<2.0dev,>=1.21.1->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (3.1.1)
    Requirement already satisfied: pyasn1-modules>=0.2.1 in /opt/conda/lib/python3.7/site-packages (from google-auth<2.0dev,>=1.21.1->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (0.2.7)
    Requirement already satisfied: rsa<5,>=3.1.4 in /opt/conda/lib/python3.7/site-packages (from google-auth<2.0dev,>=1.21.1->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (4.0)
    Requirement already satisfied: pyparsing>=2.0.2 in /opt/conda/lib/python3.7/site-packages (from packaging>=14.3->google-cloud-vision) (2.4.6)
    Requirement already satisfied: pyasn1<0.5.0,>=0.4.6 in /opt/conda/lib/python3.7/site-packages (from pyasn1-modules>=0.2.1->google-auth<2.0dev,>=1.21.1->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (0.4.8)
    Requirement already satisfied: idna<3,>=2.5 in /opt/conda/lib/python3.7/site-packages (from requests<3.0.0dev,>=2.18.0->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (2.9)
    Requirement already satisfied: chardet<4,>=3.0.2 in /opt/conda/lib/python3.7/site-packages (from requests<3.0.0dev,>=2.18.0->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (3.0.4)
    Requirement already satisfied: certifi>=2017.4.17 in /opt/conda/lib/python3.7/site-packages (from requests<3.0.0dev,>=2.18.0->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (2019.11.28)
    Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /opt/conda/lib/python3.7/site-packages (from requests<3.0.0dev,>=2.18.0->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (1.25.7)
    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m
    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m
    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m
    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m
    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m
    Requirement already satisfied: google-cloud-storage in /opt/conda/lib/python3.7/site-packages (1.29.0)
    Requirement already satisfied: google-cloud-core<2.0dev,>=1.2.0 in /opt/conda/lib/python3.7/site-packages (from google-cloud-storage) (1.6.0)
    Requirement already satisfied: google-resumable-media<0.6dev,>=0.5.0 in /opt/conda/lib/python3.7/site-packages (from google-cloud-storage) (0.5.1)
    Requirement already satisfied: google-auth<2.0dev,>=1.11.0 in /opt/conda/lib/python3.7/site-packages (from google-cloud-storage) (1.27.1)
    Requirement already satisfied: cachetools<5.0,>=2.0.0 in /opt/conda/lib/python3.7/site-packages (from google-auth<2.0dev,>=1.11.0->google-cloud-storage) (3.1.1)
    Requirement already satisfied: six>=1.9.0 in /opt/conda/lib/python3.7/site-packages (from google-auth<2.0dev,>=1.11.0->google-cloud-storage) (1.14.0)
    Requirement already satisfied: pyasn1-modules>=0.2.1 in /opt/conda/lib/python3.7/site-packages (from google-auth<2.0dev,>=1.11.0->google-cloud-storage) (0.2.7)
    Requirement already satisfied: rsa<5,>=3.1.4 in /opt/conda/lib/python3.7/site-packages (from google-auth<2.0dev,>=1.11.0->google-cloud-storage) (4.0)
    Requirement already satisfied: setuptools>=40.3.0 in /opt/conda/lib/python3.7/site-packages (from google-auth<2.0dev,>=1.11.0->google-cloud-storage) (46.1.1.post20200322)
    Requirement already satisfied: google-api-core<2.0.0dev,>=1.21.0 in /opt/conda/lib/python3.7/site-packages (from google-cloud-core<2.0dev,>=1.2.0->google-cloud-storage) (1.26.1)
    Requirement already satisfied: packaging>=14.3 in /opt/conda/lib/python3.7/site-packages (from google-api-core<2.0.0dev,>=1.21.0->google-cloud-core<2.0dev,>=1.2.0->google-cloud-storage) (20.1)
    Requirement already satisfied: pytz in /opt/conda/lib/python3.7/site-packages (from google-api-core<2.0.0dev,>=1.21.0->google-cloud-core<2.0dev,>=1.2.0->google-cloud-storage) (2019.3)
    Requirement already satisfied: requests<3.0.0dev,>=2.18.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core<2.0.0dev,>=1.21.0->google-cloud-core<2.0dev,>=1.2.0->google-cloud-storage) (2.23.0)
    Requirement already satisfied: googleapis-common-protos<2.0dev,>=1.6.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core<2.0.0dev,>=1.21.0->google-cloud-core<2.0dev,>=1.2.0->google-cloud-storage) (1.51.0)
    Requirement already satisfied: protobuf>=3.12.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core<2.0.0dev,>=1.21.0->google-cloud-core<2.0dev,>=1.2.0->google-cloud-storage) (3.12.2)
    Requirement already satisfied: pyparsing>=2.0.2 in /opt/conda/lib/python3.7/site-packages (from packaging>=14.3->google-api-core<2.0.0dev,>=1.21.0->google-cloud-core<2.0dev,>=1.2.0->google-cloud-storage) (2.4.6)
    Requirement already satisfied: pyasn1<0.5.0,>=0.4.6 in /opt/conda/lib/python3.7/site-packages (from pyasn1-modules>=0.2.1->google-auth<2.0dev,>=1.11.0->google-cloud-storage) (0.4.8)
    Requirement already satisfied: idna<3,>=2.5 in /opt/conda/lib/python3.7/site-packages (from requests<3.0.0dev,>=2.18.0->google-api-core<2.0.0dev,>=1.21.0->google-cloud-core<2.0dev,>=1.2.0->google-cloud-storage) (2.9)
    Requirement already satisfied: chardet<4,>=3.0.2 in /opt/conda/lib/python3.7/site-packages (from requests<3.0.0dev,>=2.18.0->google-api-core<2.0.0dev,>=1.21.0->google-cloud-core<2.0dev,>=1.2.0->google-cloud-storage) (3.0.4)
    Requirement already satisfied: certifi>=2017.4.17 in /opt/conda/lib/python3.7/site-packages (from requests<3.0.0dev,>=2.18.0->google-api-core<2.0.0dev,>=1.21.0->google-cloud-core<2.0dev,>=1.2.0->google-cloud-storage) (2019.11.28)
    Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /opt/conda/lib/python3.7/site-packages (from requests<3.0.0dev,>=2.18.0->google-api-core<2.0.0dev,>=1.21.0->google-cloud-core<2.0dev,>=1.2.0->google-cloud-storage) (1.25.7)
    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m
    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m
    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m



```python
!pip3 install --upgrade google-cloud-vision
```

    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m
    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m
    Requirement already satisfied: google-cloud-vision in /opt/conda/lib/python3.7/site-packages (2.4.0)
    Requirement already satisfied: google-api-core[grpc]<2.0.0dev,>=1.26.0 in /opt/conda/lib/python3.7/site-packages (from google-cloud-vision) (1.26.1)
    Requirement already satisfied: proto-plus>=1.15.0 in /opt/conda/lib/python3.7/site-packages (from google-cloud-vision) (1.15.0)
    Requirement already satisfied: packaging>=14.3 in /opt/conda/lib/python3.7/site-packages (from google-cloud-vision) (20.1)
    Requirement already satisfied: six>=1.13.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (1.14.0)
    Requirement already satisfied: setuptools>=40.3.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (46.1.1.post20200322)
    Requirement already satisfied: protobuf>=3.12.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (3.12.2)
    Requirement already satisfied: pytz in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (2019.3)
    Requirement already satisfied: requests<3.0.0dev,>=2.18.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (2.23.0)
    Requirement already satisfied: google-auth<2.0dev,>=1.21.1 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (1.27.1)
    Requirement already satisfied: googleapis-common-protos<2.0dev,>=1.6.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (1.51.0)
    Requirement already satisfied: grpcio<2.0dev,>=1.29.0 in /opt/conda/lib/python3.7/site-packages (from google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (1.37.0)
    Requirement already satisfied: cachetools<5.0,>=2.0.0 in /opt/conda/lib/python3.7/site-packages (from google-auth<2.0dev,>=1.21.1->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (3.1.1)
    Requirement already satisfied: pyasn1-modules>=0.2.1 in /opt/conda/lib/python3.7/site-packages (from google-auth<2.0dev,>=1.21.1->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (0.2.7)
    Requirement already satisfied: rsa<5,>=3.1.4 in /opt/conda/lib/python3.7/site-packages (from google-auth<2.0dev,>=1.21.1->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (4.0)
    Requirement already satisfied: pyparsing>=2.0.2 in /opt/conda/lib/python3.7/site-packages (from packaging>=14.3->google-cloud-vision) (2.4.6)
    Requirement already satisfied: pyasn1<0.5.0,>=0.4.6 in /opt/conda/lib/python3.7/site-packages (from pyasn1-modules>=0.2.1->google-auth<2.0dev,>=1.21.1->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (0.4.8)
    Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /opt/conda/lib/python3.7/site-packages (from requests<3.0.0dev,>=2.18.0->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (1.25.7)
    Requirement already satisfied: certifi>=2017.4.17 in /opt/conda/lib/python3.7/site-packages (from requests<3.0.0dev,>=2.18.0->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (2019.11.28)
    Requirement already satisfied: idna<3,>=2.5 in /opt/conda/lib/python3.7/site-packages (from requests<3.0.0dev,>=2.18.0->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (2.9)
    Requirement already satisfied: chardet<4,>=3.0.2 in /opt/conda/lib/python3.7/site-packages (from requests<3.0.0dev,>=2.18.0->google-api-core[grpc]<2.0.0dev,>=1.26.0->google-cloud-vision) (3.0.4)
    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m
    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m
    [33mWARNING: Ignoring invalid distribution -oogle-cloud-datastore (/opt/conda/lib/python3.7/site-packages)[0m

