[elastalink-3f10-ml_ai] Details
============================

Generated On: 2025-02-11 14:23:33 UTC

TML Solution DAG Parameters' Details: User Chosen Parametets
----------------------------

STEP 1: Get TML Core Params: `tml_system_step_1_getparams_dag <https://tml.readthedocs.io/en/latest/tmlbuilds.html#step-1-get-tml-core-params-tml-system-step-1-getparams-dag>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::

   * - **User Parameter**
     - **Chosen Value**
   * - solutionname
     - elastalink-3f10-ml_ai
   * - solutiontitle
     - ElastaLink TML Solution
   * - solutiondescription
     - This is an awesome real-time solution built by TSS for ElastaLink
   * - brokerhost
     - 127.0.0.1
   * - brokerport
     - 9092
   * - cloudusername
     - None
   * - ingestdatamethod
     - LOCALFILE
 
STEP 2: Create Kafka Topics: `tml_system_step_2_kafka_createtopic_dag <https://tml.readthedocs.io/en/latest/tmlbuilds.html#step-2-create-kafka-topics-tml-system-step-2-kafka-createtopic-dag>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::

   * - **User Parameter**
     - **Chosen Value**
   * - companyname
     - Otics
   * - myname
     - Sebastian
   * - myemail
     - Sebastian.Maurice
   * - mylocation
     - Toronto
   * - replication
     - 1
   * - numpartitions
     - 1
   * - enabletls
     - 1
   * - microserviceid
     - 
   * - raw_data_topic
     - iot-raw-data
   * - preprocess_data_topic
     - iot-preprocess,iot-preprocess2
   * - ml_data_topic
     - ml-data
   * - prediction_data_topic
     - prediction-data

STEP 3: `Produce to Kafka Topics <https://tml.readthedocs.io/en/latest/tmlbuilds.html#step-3-produce-to-kafka-topics>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::

   * - **User Parameter**
     - **Chosen Value**
   * - PRODUCETYPE
     - LOCALFILE
   * - TOPIC
     - iot-raw-data
   * - PORT
     - _39399
   * - IDENTIFIER
     - TML solution for Elastalink,/rawdata/elastalink/networkLogs2.txt
   * - HTTPADDR
     - https://
   * - FROMHOST
     - ('seb', '127.0.1.1')
   * - TOHOST
     - 0.0.0.0
   * - CLIENTPORT
     - Not Applicable
   * - TSS_CLIENTPORT
     - Not Applicable
   * - TML_CLIENTPORT
     - Not Applicable

STEP 4: Preprocesing Data: `tml-system-step-4-kafka-preprocess-dag <https://tml.readthedocs.io/en/latest/tmlbuilds.html#step-4-preprocesing-data-tml-system-step-4-kafka-preprocess-dag>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::

   * - **User Parameter**
     - **Chosen Value**
   * - raw_data_topic
     - iot-raw-data
   * - preprocess_data_topic
     - iot-preprocess,iot-preprocess2
   * - preprocessconditions
     - 
   * - delay
     - 70
   * - array
     - 0
   * - saveasarray
     - 1
   * - topicid
     - -999
   * - rawdataoutput
     - 1
   * - asynctimeout
     - 120
   * - timedelay
     - 0
   * - preprocesstypes
     - anomprob,trend,avg
   * - pathtotmlattrs
     - --pathtotmlattrs--
   * - identifier
     - IoT device performance and failures
   * - jsoncriteria
     - uid=metadata.dsn,filter:allrecords~subtopics=metadata.property_name~values=datapoint.value~identifiers=metadata.display_name~datetime=datapoint.created_at~msgid=datapoint.id~latlong=lat:long

STEP 4b: Preprocesing Data: `tml-system-step-4b-kafka-preprocess-dag <https://tml.readthedocs.io/en/latest/tmlbuilds.html#step-4b-preprocesing-data-tml-system-step-4b-kafka-preprocess-dag>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::

   * - **User Parameter**
     - **Chosen Value**
   * - raw_data_topic
     - --raw_data_topic2--
   * - preprocess_data_topic
     - --preprocess_data_topic2--
   * - preprocessconditions
     - --preprocessconditions2--
   * - delay
     - --delay2--
   * - array
     - --array2--
   * - saveasarray
     - --saveasarray2--
   * - topicid
     - --topicid2--
   * - rawdataoutput
     - --rawdataoutput2--
   * - asynctimeout
     - --asynctimeout2--
   * - timedelay
     - --timedelay2--
   * - preprocesstypes
     - --preprocesstypes2--
   * - pathtotmlattrs
     - --pathtotmlattrs2--
   * - identifier
     - --identifier2--
   * - jsoncriteria
     - --jsoncriteria2--

STEP 5: Entity Based Machine Learning : `tml-system-step-5-kafka-machine-learning-dag <https://tml.readthedocs.io/en/latest/tmlbuilds.html#step-5-entity-based-machine-learning-tml-system-step-5-kafka-machine-learning-dag>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::

   * - **User Parameter**
     - **Chosen Value**
   * - preprocess_data_topic
     - iot-preprocess,iot-preprocess2
   * - ml_data_topic
     - ml-data
   * - modelruns
     - 100
   * - offset
     - -1
   * - islogistic
     - 1
   * - networktimeout
     - 600
   * - modelsearchtuner
     - 90
   * - processlogic
     - classification_name=failure_prob:Power_preprocessed_AnomProb=55,n
   * - dependentvariable
     - failure
   * - independentvariables
     - Power_preprocessed_AnomProb
   * - rollbackoffsets
     - 1000
   * - topicid
     - -999
   * - consumefrom
     - 
   * - fullpathtotrainingdata
     - /Viper-ml/viperlogs/iotlogistic
   * - transformtype
     - 
   * - sendcoefto
     - 
   * - coeftoprocess
     - 
   * - coefsubtopicnames
     - 

STEP 6: Entity Based Predictions: `tml-system-step-6-kafka-predictions-dag <https://tml.readthedocs.io/en/latest/tmlbuilds.html#step-6-entity-based-predictions-tml-system-step-6-kafka-predictions-dag>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::

   * - **User Parameter**
     - **Chosen Value**
   * - preprocess_data_topic
     - iot-preprocess,iot-preprocess2
   * - ml_prediction_topic
     - iot-ml-prediction-results-output
   * - streamstojoin
     - Power_preprocessed_AnomProb
   * - inputdata
     - 
   * - consumefrom
     - ml-data
   * - offset
     - -1
   * - delay
     - 70
   * - usedeploy
     - 1
   * - networktimeout
     - 600
   * - maxrows
     - 50
   * - topicid
     - -999
   * - pathtoalgos
     - /Viper-ml/viperlogs/iotlogistic

STEP 7: Real-Time Visualization: `tml-system-step-7-kafka-visualization-dag <https://tml.readthedocs.io/en/latest/tmlbuilds.html#step-7-real-time-visualization-tml-system-step-7-kafka-visualization-dag>`_
^^^^^^^^^^^^^^^^^^^^^

.. list-table::

   * - **User Parameter**
     - **Chosen Value**
   * - vipervizport
     - 49689
   * - topic
     - iot-preprocess,iot-preprocess2
   * - dashboardhtml
     - dashboard.html
   * - secure
     - 1
   * - offset
     - -1
   * - append
     - 0
   * - chip
     - amd64
   * - rollbackoffset
     - 400

STEP 8: `tml_system_step_8_deploy_solution_to_docker_dag <https://tml.readthedocs.io/en/latest/tmlbuilds.html#step-8-deploy-tml-solution-to-docker-tml-system-step-8-deploy-solution-to-docker-dag>`_
^^^^^^^^^^^^^^^^^^^^^
.. list-table::

   * - **User Parameter**
     - **Chosen Value**
   * - Docker Container
     - maadsdocker/elastalink-3f10-ml_ai-amd64 (https://hub.docker.com/r/maadsdocker/elastalink-3f10-ml_ai-amd64)
   * - Docker Run Command
     - docker run -d -p 5050:5050 -p 4040:4040 -p 6060:6060 \
          --env TSS=0 \
          --env SOLUTIONNAME=elastalink-3f10-ml_ai \
          --env SOLUTIONDAG=solution_preprocessing_ml_ai_dag-elastalink-3f10 \
          --env GITUSERNAME=smaurice101  \
          --env GITREPOURL=https://github.com/smaurice101/raspberrypitss.git \
          --env SOLUTIONEXTERNALPORT=5050 \
          -v /var/run/docker.sock:/var/run/docker.sock:z \
          -v /your_localmachine/foldername:/rawdata:z \
          --env CHIP=amd64 \
          --env SOLUTIONAIRFLOWPORT=4040 \
          --env SOLUTIONVIPERVIZPORT=6060 \
          --env DOCKERUSERNAME='maadsdocker' \
          --env EXTERNALPORT=39399 \
          --env KAFKACLOUDUSERNAME='MUHRHBPKJYPROKBX' \
          --env VIPERVIZPORT=49689 \
          --env MQTTUSERNAME='smaurice' \
          --env AIRFLOWPORT=9000 \
          --env MQTTPASSWORD='<Enter mqtt password>' \
          --env KAFKACLOUDPASSWORD='<Enter API secret>' \
          --env GITPASSWORD='<Enter Github Password>' \
          --env READTHEDOCS='<Enter Readthedocs token>' \
          maadsdocker/elastalink-3f10-ml_ai-amd64

STEP 9: `tml_system_step_9_privategpt_qdrant_dag <https://tml.readthedocs.io/en/latest/tmlbuilds.html#step-9-privategpt-and-qdrant-integration-tml-system-step-9-privategpt-qdrant-dag>`_
^^^^^^^^^^^^^^^^^^^^^
.. list-table::

   * - **User Parameter**
     - **Chosen Value**
   * - PrivateGPT Container
     - maadsdocker/tml-privategpt-with-gpu-nvidia-amd64-v2
   * - PrivateGPT Run Command
     - docker run -d -p 8001:8001 --net=host --gpus all --env PORT=8001 --env GPU=1 --env COLLECTION=tml-llm-model-v2 --env WEB_CONCURRENCY=2 --env CUDA_VISIBLE_DEVICES=0 maadsdocker/tml-privategpt-with-gpu-nvidia-amd64-v2
   * - Qdrant Container
     - qdrant/qdrant
   * - Qdrant Run Command
     - docker run -d -p 6333:6333 -v $(pwd)/qdrant_storage:/qdrant/storage:z qdrant/qdrant
   * - Consumefrom
     - 
   * - pgpt_data_topic
     - cisco-network-privategpt
   * - offset
     - -1
   * - rollbackoffset
     - 400
   * - topicid
     - -999
   * - enabletls
     - 1
   * - partition
     - -1
   * - prompt
     - [INST] Are there any errors in the  logs? Give s detailed response including IP addresses and host machines.[/INST]
   * - context
     - This is network data from inbound and outbound packets. The data are anomaly probabilities for cyber threats from analysis of inbound and outbound packets. If inbound or outbound anomaly probabilities are less than 0.60, it is likely the risk of a cyber attack is also low. If its above 0.60, then risk is mid to high.
   * - jsonkeytogather
     - hyperprediction
   * - keyattribute
     - inboundpackets,outboundpackets
   * - keyprocesstype
     - anomprob
   * - vectordbcollectionname
     - tml-llm-model-v2
   * - concurrency
     - 2
   * - CUDA_VISIBLE_DEVICES
     - 0
   * - pgpthost
     - http://127.0.0.1
   * - pgptport
     - 8001
   * - hyperbatch
     - 0
   * - docfolder
     - mylogs,mylogs2
   * - docfolderingestinterval
     - 900
   * - useidentifierinprompt
     - 1
   * - searchterms
     - 192.168.--identifier--,authentication failure
   * - streamall
     - 1
   * - temperature
     - 0.1
   * - vectorsearchtype
     - Manhattan
   * - llm
     - Refer to: https://tml.readthedocs.io/en/latest/genai.html
   * - embedding
     - Refer to: https://tml.readthedocs.io/en/latest/genai.html
   * - vectorsize
     - Refer to: https://tml.readthedocs.io/en/latest/genai.html

STEP 10: `tml_system_step_10_documentation_dag <https://tml.readthedocs.io/en/latest/tmlbuilds.html#step-10-create-tml-solution-documentation-tml-system-step-10-documentation-dag>`_
^^^^^^^^^^^^^^^^^^^^^
.. list-table::

   * - **User Parameter**
     - **Chosen Value**
   * - Solution Documentation URL
     - https://elastalink-3f10-ml_ai.readthedocs.io
