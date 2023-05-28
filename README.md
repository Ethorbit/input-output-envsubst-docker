# input-output-envsubst
Set input, output directory and file extension to expand environment variables in all files.

# Example
docker cli:
```sh
docker run -it --rm --name my_envsubst \
    -e FILE_EXTENSION='cfg' \
    -v ./data/raw_files:/input \
    -v ./data/formatted_files:/output \
    --network 'none' \
    --cap-drop=ALL \
    --cap-add=DAC_OVERRIDE \
    --cap-add=FOWNER \
    ethorbit/input-output-envsubst:v1.0
```

docker-compose:
```yaml
services:
    my_envsubst:
        image: ethorbit/input-output-envsubst:v1.0
        environment:
            - FILE_EXTENSION='cfg'
        volumes:
            - ./data/raw_files:/input
            - ./data/formatted_files:/output
        network_mode: none
        cap_drop:
            - ALL
        cap_add:
            - DAC_OVERRIDE
            - FOWNER
        restart: on-failure
```

In this example we expand all environment variables contained in .cfg files in the relative `./data/raw_files` directory and output the expanded files to `./data/formatted_files`. The files in `raw_files` remain untouched.

# What is this used for
This is used when you need to put environment variables into service config files. In my time of using Docker, this is something I've needed to do many times and having an image built for that purpose makes things a lot less repetitive.
