AWSTemplateFormatVersion: 2010-09-09
Resources:
  S3Bucket:
    Type: 'AWS::S3::Bucket'
    Properties:
      BucketName: newtestbucketlc
      AccessControl: Private
      LifecycleConfiguration:
        Rules:
          - Id: StandardOneZoneIA
            Prefix: glacierflexibleretrieval
            ExpiredObjectDeleteMarker: true
            Status: Enabled
            Transitions:
              - TransitionInDays: 35
                StorageClass: STANDARD_IA
          - Id: GlacierInstantRetrievalRule
            Prefix: GlacierInstantRetrieval
            Status: Enabled
            ExpirationInDays: 700
            Transitions:
              - TransitionInDays: 95
                StorageClass: GLACIER_IR
          - Id: GlacierFlexibleRetrievalRule
            Prefix: GlacierFlexibleRetrieval
            Status: Enabled
            ExpirationInDays: 95
            Transitions:
                - TransitionInDays: 35
                  StorageClass: GLACIER      
Outputs:
  BucketName:
    Value: !Ref S3Bucket
    Description: Name of the sample Amazon S3 bucket with a lifecycle configuration.
