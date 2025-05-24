 
# Payrix OpenAPI specification

This is the "golden", one source of truth API specification


## Running the linter
We are using the Redocly [Redocly-cli](https://redocly.com/docs/cli/commands/lint) as a guide enforcer and linter. 
Installations instructions are on [their site](https://github.com/Redocly/redocly-cli).

There is a `.redocly.yaml` file already in the top level of the directory. This is where we specify rules that the linter
should check. Redocly has quite a flexible system for making rules but they also have a lot of [rules](hhttps://redocly.com/docs/cli/guides/configure-rules) out of [the box](https://redocly.com/docs/cli/rules/minimal). There are also recommendations, with examples, 
on how to [specify](https://redocly.com/docs/cli/rules/configurable-rules) the rules.

Once you have installed the CLI running the linter is as simple as: 

```shell
redocly lint openapi.yaml 
```

This will send the results to the screen. If you would like to save the results in a file you can run

```shell
redocly lint openapi.yaml  > output.log
```

This will overwrite an existing output.log and put the results of the command in the file. 


## Generating a single HTML preview of the documentation

You can use the [Redocly CLI](https://redocly.com/docs/cli/) to generate a single long html document for the API.
The CLI is [installed](https://redocly.com/docs/cli/installation/) using NPM and is quite straightforward. 

Once that is complete you just run:

```shell
redocly build-docs ./openapi.yaml
```

It uses the tags for the URL operations (POST, GET...) from tags on each operation. These tags are used to group URLs into 
categories for the left nav. 
By default, redocly does not sort these categories alphabetically. To get it sorted alphabetically run:

```shell
redocly build-docs ./openapi.yaml --theme.openapi.sortTagsAlphabetically
```

When you run the command it will generate some errors in the terminal. You can ignore them, the output doc is still produced.
You can change other output features by [adding more](https://redocly.com/docs/api-reference-docs/configuration/functionality/) --theme.openapi.XXXXX to the command. 

