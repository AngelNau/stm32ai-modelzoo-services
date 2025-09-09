# stm32ai-modelzoo-services
This directory contains all the necessary files for deploying the model on the STM32H747I-Discovery board. It also contains the [application code](./stm32ai-modelzoo-services/application_code/image_classification/STM32H7/) used when writing the thesis.

## Running the script

The script used is [stm32ai_main.py](stm32ai-modelzoo-services/image_classification/stm32ai_main.py) with
the configuration file for [deployment](stm32ai-modelzoo-services/image_classification/src/config_file_examples/deployment_config.yaml).

Before running the script, make sure you have a myST account, if not, you can create one [here](https://www.st.com/content/st_com/en/user-registration.html). Also make sure to set the STM32CubeIDE path in the [configuration file](stm32ai-modelzoo-services/image_classification/src/config_file_examples/deployment_config.yaml).
Make sure the STM32H747I-Discovery board is connected along with the B-CAMS-OMV camera module bundle.

Assuming that a virtual environment already exists and is activated, the code can be run using:
```bash
cd image_classification/
python stm32ai_main.py --config-path ./src/config_file_examples/ --config-name deployment_config.yaml
```

## Flashing manually
If the script didn't flash the project on the board, start up `STM32CubeIDE` and import the project manually. The directory to use when importing the project is `/intelligent-embedded-system/stm32ai-modelzoo-services/application_code/image_classification/STM32H7/Application/STM32H747I-DISCO/STM32CubeIDE/` ([link to directory](stm32ai-modelzoo-services/application_code/image_classification/STM32H7/Application/STM32H747I-DISCO/STM32CubeIDE/)).

After successfully importing into STM32CubeIDE, simply build and run the `STM32H747I-DISCO_GettingStarted_ImageClassification_CM7` project.

## Known errors
Upon getting an error like:\
`ImportError: /intelligent-embedded-system/stm32ai-modelzoo-services/.venv/lib/python3.10/site-packages/onnxruntime/capi/onnxruntime_pybind11_state.cpython-310-x86_64-linux-gnu.so: cannot enable executable stack as shared object requires: Invalid argument`.\
Run the following command in the directory where you initiated the virtual environment:
```bash
execstack -c .venv/lib/python3.10/site-packages/onnxruntime/capi/onnxruntime_pybind11_state.cpython-310-x86_64-linux-gnu.so
```
Make sure the python version is set correctly in the command above.