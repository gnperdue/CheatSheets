
gcloud auth list
gcloud config list project
gcloud config set compute/zone us-central1-a
gcloud container clusters create awwvision \
    --num-nodes 2 \
    --scopes cloud-platform

gcloud container clusters get-credentials awwvision

gcloud ai-platform models create flights --regions us-central1
gcloud ai-platform versions create v1 --model flights \
                                      --origin ${MODEL_LOCATION} \
                                      --runtime-version 1.10

kubectl cluster-info
kubectl get pods
kubectl get deployments -o wide

export PROJECT_ID=$(gcloud info --format='value(config.project)')
export BUCKET=${PROJECT_ID}

gsutil cp gs://${BUCKET}/flights/chapter9/linear-model.tar.gz ~
MODEL_LOCATION=$(gsutil ls $OUTPUT_DIR/export/exporter | tail -1)

gsutil mv -p gs://gnpqwiklabs_cloudstorageconsole/800px-Ada_Lovelace_portrait.jpg gs://gnpqwiklabs_cloudstorageconsole/ada.jpg
gsutil mv -p gs://gnpqwiklabs_cloudstorageconsole/folder1/folder2/800px-Ada_Lovelace_portrait.jpg gs://gnpqwiklabs_cloudstorageconsole/folder1/folder2/


export JOBNAME=dnn_flights_$(date -u +%y%m%d_%H%M%S)

gcloud ml-engine jobs submit training $JOBNAME \
  --module-name=trainer.task \
  --package-path=$(pwd)/flights/trainer \
  --job-dir=$OUTPUT_DIR \
  --staging-bucket=gs://$BUCKET \
  --region=$REGION \
  --scale-tier=STANDARD_1 \
  --runtime-version=1.10 \
  -- \
  --output_dir=$OUTPUT_DIR \
  --traindata $DATA_DIR/train* --evaldata $DATA_DIR/test*


gcloud ml-engine jobs submit training $JOBNAME \
  --module-name=trainer.task \
  --package-path=$(pwd)/flights/trainer \
  --job-dir=$OUTPUT_DIR \
  --staging-bucket=gs://$BUCKET \
  --region=$REGION \
  --scale-tier=STANDARD_1 \
  --runtime-version=1.10 \
  -- \
  --output_dir=$OUTPUT_DIR \
  --traindata $DATA_DIR/train* --evaldata $DATA_DIR/test*

WARNING: The `gcloud ml-engine` commands have been renamed and will soon be removed. Please use `gcloud ai-platform` instead.

sudo pip install --upgrade google-api-python-client
sudo pip install --upgrade oauth2client


gcloud container clusters get-credentials burt-kubeflow --zone us-central1-a --project fermilab-nord-ldrd \
 && kubectl port-forward --namespace kubeflow $(kubectl get pod --namespace kubeflow --selector="service=ambassador" --output jsonpath='{.items[0].metadata.name}') 8080:80


export BUCKET_NAME=kubeflow-${PROJECT_ID}
gsutil mb gs://${BUCKET_NAME}

gcloud config set core/project $PROJECT_ID
gcloud config set compute/zone us-central1-f
gsutil mb -c multi_regional -l us gs://gnp-housing-predict
datalab create my-datalab --machine-type n1-standard-4

gcloud ai-platform jobs describe housing_190826_224933
gcloud ai-platform jobs stream-logs housing_190826_224933

