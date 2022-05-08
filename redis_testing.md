Ping Test (ping_test.json)
memtier_benchmark --clients 50 --threads 4 --requests 10000 --pipeline 1 --json-out-file ping2_test.json --command "PING" -p 6360 --hdr-file-prefix

Get Set manual test (I think this is a 50-50 split) (set_get_test.json)
memtier_benchmark --clients 50 --threads 4 --requests 10000 --pipeline 1 --json-out-file set2_get_test.json --command "SET foo "bar"" --command "GET foo" -p 6360 --hdr-file-prefix 

Default test (default_test.json)
memtier_benchmark --clients 50 --threads 4 --requests 10000 --pipeline 1 --json-out-file default2_test_1.json -p 6360 --hdr-file-prefix

This adds renet50.pb with mymodel as its key to redis
cat resnet50.pb | redis-cli -p 6360 -x AI.MODELSTORE mymodel TF CPU TAG imagenet:5.0 INPUTS 1 images OUTPUTS 1 output BLOB

memtier_benchmark --clients 50 --threads 4 --requests 10000 --pipeline 1 --json-out-file ai_model1.json --command "AI.MODELEXECUTE mymodel INPUTS 1 images OUTPUTS 1 BLOB" -p 6360 --hdr-file-prefix