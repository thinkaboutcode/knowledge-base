architecture-beta
group mlops_pipeline(logos:aws-lambda)[ML Ops Pipeline]

    service data_ingest(logos:aws-kinesis)[Data Ingestion] in mlops_pipeline
    service s3_raw(logos:aws-s3)[Raw Data Storage] in mlops_pipeline
    service s3_processed(logos:aws-s3)[Processed Data Storage] in mlops_pipeline
    service data_processing(logos:aws-glue)[Data Processing] in mlops_pipeline
    service model_training(logos:aws-sagemaker)[Model Training] in mlops_pipeline
    service model_registry(logos:aws-ecr)[Model Registry] in mlops_pipeline
    service inference_endpoint(logos:aws-lambda)[Inference Endpoint] in mlops_pipeline
    service api_gateway(logos:aws-apigateway)[API Gateway] in mlops_pipeline

    data_ingest:T -- B:s3_raw
    s3_raw:T -- B:data_processing
    data_processing:T -- B:s3_processed
    s3_processed:T -- B:model_training
    model_training:T -- B:model_registry
    model_registry:T -- B:inference_endpoint
    inference_endpoint:T -- B:api_gateway
