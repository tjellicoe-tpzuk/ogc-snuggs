# s-expression for EO product band math


## Development 

```bash
cd app-s-expression
```

Create the Python environment with `mamba` (faster) or `conda` (slower):

```bash
mamba env create -f environment.yml
```

Activate the Python environment with:

```bash
conda activate env_app_snuggs
```

### Build the Python project

To build and install the project locally:

```
python setup.py install
```

Test the CLI with:

```bash
s-expression --help
```

That returns:

```console
$ s-expression --help
Usage: s-expression [OPTIONS]

  Applies s expressions to EO acquisitions

Options:
  -i, --input_reference PATH  Input product reference  [required]
  -s, --s-expression TEXT     s expression  [required]
  -b, --cbn TEXT              Common band name  [required]
  --help                      Show this message and exit.
```

### Build the container

```console
docker build . -t snuggs
```

### Execution

We provide two example sets of parameters you may wish to use when testing this application package: `params.yml` and `more-params.yml`. The first of which is simpler and only requires you to specify the BANDS you are concerned with inside your s_expression(s) inputs. The band names are extracted from the input expression and searched for within the assets of the provide STAC items. If instead your BANDS are provided inside assets of a different name you can specify this as an additional input to the workflow: `assets`. 
The STAC items need to include assets that are readable using gdal in python, `ds = gdal.Open(<asset-reference>)`, with the bands then accessible by the `GetRasterBand(<band-index>)` function.

```console
cwltool --parallel app-package.cwl#s-expression params.yml
```

## Releases

Releases are published in https://github.com/EOEPCA/app-snuggs/releases

