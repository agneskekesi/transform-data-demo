# Transform Metrics Demo
Welcome to your new Tansform Project! See full install instructions on the [install page](https://app.transformdata.io/install) to get started using Transform.

## Resources
* Learn more about Transform [in the docs](https://www.notion.so/transformdata/Transform-Documentation-4eb96a3207634834ab1ae8b5b23923ff)
* Reach out to our team at [support@transformdata.io](mailto:support@transformdata.io) for support or to setup a shared slack channel

## Congifure Github Workflows
Transform uses Github Workflows to validate and commit new versions of your metrics configs to our service. In this template repo, we've already set up these workflows for you in the `/.github` directory.

By default, we will run validation checks on open PRs, and commit new metric configs to Transform whenever a new commit is merged to the `main` branch.

You'll need to save the Transform API key for your Service User within the [Github Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository) for this repo under `TRANSFORM_API_KEY={TRANSFORM_API_KEY}` for the above actions to work properly.


## CLI Quick Start Guide

Some users prefer to set up a Python virtual environment in this directory, though this is optional:
```
python3 -m venv venv && source venv/bin/activate
```

1. Install the Transform client CLI:
```
pip install transform
```

2. To authenticate to Transform MQL server using the CLI, navigate to this directory and run
```
mql setup -k your_api_key
```
You will be asked to provide the API you created during setup, so have it handy.

## CLI Quick Start Guide with poetry
> Skip this if you've already use virtual env above

- To start development, make sure you're in shell:
    ```
    python3 -m poetry shell
    ```
    BUT before that, let's follow the setup guidline at the first time.

- Prequisites:
    - Install Python 3.9.6+ as recommended (specified in [pyproject.toml](pyproject.toml)) 
        > Assuming your python alias: `python3`

        > Don't need to use alias if your enviroment is not multi python version

    - Install `poetry`
    ```
    python3 -m pip install poetry
    ```

- Install the dependencies and go into shell:
    ```
    python3 -m poetry install && python3 -m poetry shell
    ```
    > NOTE: Currently it's experiencing an issue with pandas install within poetry - it might take ~5 mins to install. See: https://github.com/pandas-dev/pandas/issues/40611

- Verify if you're ready:
    ```
    mql version
    ```

- To authenticate to Transform MQL server using the CLI, navigate to this directory and run
  ```
  mql setup -k <your_api_key>
  ```
  You will be asked to provide the API you created during setup, so have it handy.

## MQL CLI Example
Below is a list of common MQL commands.

List all metrics available:
```
mql list-metrics
```

Run the `revenue_usd` metric by day:
```
mql query --metrics revenue_usd --dimensions ds
```

Change the output to be odered by decending day:
```
mql query --metrics revenue_usd --dimensions ds --order -ds
```

Add the `country` dimension from the separate `customer` data source. Notice the `__` to indicate the join identifier:
```
mql query --metrics revenue_usd --dimensions ds --dimensions customer__country --order -ds
```

Run a ratio metric:
```
mql query --metrics cancellation_rate --dimensions ds --order -ds
```