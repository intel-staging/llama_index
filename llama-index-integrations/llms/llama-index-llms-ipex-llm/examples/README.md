# IpexLLM Examples

This folder contains examples showcasing how to use LlamaIndex with `ipex-llm` LLM integration `llama_index.llms.ipex_llm.IpexLLM`.

## Installation

### On CPU

Install `llama-index-llms-ipex-llm`. This will also install `ipex-llm` and its dependencies.

```bash
pip install llama-index-llms-ipex-llm
```

### On GPU

Install `llama-index-llms-ipex-llm`. This will also install `ipex-llm` and its dependencies.

```bash
pip install llama-index-llms-ipex-llm[xpu] --extra-index-url https://pytorch-extension.intel.com/release-whl/stable/xpu/us/
```

## List of Examples

### Basic Example

The example [basic.py](./basic.py) shows how to run `IpexLLM` on Intel CPU or GPU and conduct tasks such as text completion. Run the example as following:

```bash
python basic.py -m <path_to_model> -d <cpu_or_xpu> -q <query_to_LLM>
```

> Please note that in this example we'll use [HuggingFaceH4/zephyr-7b-alpha](https://huggingface.co/HuggingFaceH4/zephyr-7b-alpha) model for demonstration. It requires updating `transformers` and `tokenizers` packages.
>
> ```bash
> pip install -U transformers==4.37.0 tokenizers==0.15.2
> ```

### Low Bit Example

The example [low_bit.py](./low_bit.py) shows how to save and load low_bit model by `IpexLLM` on Intel CPU or GPU and conduct tasks such as text completion. Run the example as following:

```bash
python low_bit.py -m <path_to_model> -d <cpu_or_xpu> -q <query_to_LLM> -s <save_low_bit_dir>
```

> Please note that in this example we'll use [HuggingFaceH4/zephyr-7b-alpha](https://huggingface.co/HuggingFaceH4/zephyr-7b-alpha) model for demonstration. It requires updating `transformers` and `tokenizers` packages.
>
> ```bash
> pip install -U transformers==4.37.0 tokenizers==0.15.2
> ```

### More Data Types Example

By default, `IpexLLM` loads the model in int4 format. To load a model in different data formats like `sym_int5`, `sym_int8`, etc., you can use the `load_in_low_bit` option in `IpexLLM`. To load a model on different device like `cpu` or `xpu`, you can use the `device_map` option in `IpexLLM`.

The example [more_data_type.py](./more_data_type.py) shows how to use the `load_in_low_bit` option and `device_map` option. Run the example as following:

```bash
python more_data_type.py -m <path_to_model> -t <path_to_tokenizer> -l <low_bit_format> -d <device> -q <query_to_LLM>
```

> Note: If you're using [meta-llama/Llama-2-7b-hf](https://huggingface.co/meta-llama/Llama-2-7b-hf) model in this example, it is recommended to use transformers version
> <=4.34.

### Text2SQL Example

This example [text2sql](./text2sql.py) demonstrates how to use LlamaIndex with `ipex-llm` to run a text-to-SQL model on Intel hardware. This example shows how to create a database, define a schema, and run SQL queries using low-bit model optimized with `ipex-llm`.

### Setup

It requires `llama-index-embeddings-ipex-llm` package as it uses `ipex-llm` embedding.

> ```bash
> pip install llama-index-embeddings-ipex-llm
> ```

#### Runtime Configurations

For optimal performance, it is recommended to set several environment variables based on your device:

- For Windows Users with Intel Core Ultra integrated GPU
  In Anaconda Prompt:

  > > ```
  > > set SYCL_CACHE_PERSISTENT=1
  > > set BIGDL_LLM_XMX_DISABLED=1
  > > ```

- For Linux Users with Intel Arc A-Series GPU:
  > > ```
  > > # Configure oneAPI environment variables. Required step for APT or offline installed oneAPI.
  > > # Skip this step for PIP-installed oneAPI since the environment has already been configured in LD_LIBRARY_PATH.
  > > source /opt/intel/oneapi/setvars.sh
  > >
  > > # Recommended Environment Variables for optimal performance
  > > export USE_XETLA=OFF
  > > export SYCL_PI_LEVEL_ZERO_USE_IMMEDIATE_COMMANDLISTS=1
  > > export SYCL_CACHE_PERSISTENT=1
  > > ```

> **NOTE** For the first time that each model runs on Intel iGPU/Intel Arc A300-Series or Pro A60, it may take several minutes to compile.

---

### Run the Example

Then, run the example as following:

```
python text2sql.py -m <path_to_model> -d <device> -e <path_to_embedding_model> -q <query_to_LLM> -n <num_predict>
```

> Please note that in this example we'll use [meta-llama/Meta-Llama-3-8B](https://huggingface.co/meta-llama/Meta-Llama-3-8B) model for demonstration, as well as [bge-large-en-v1.5](https://huggingface.co/BAAI/bge-large-en-v1.5) for our embedding model. It requires updating transformers and tokenizers packages. But you are also welcomed to use other models.

> If you use other LLMs and encounter output issues, please try changing it.
