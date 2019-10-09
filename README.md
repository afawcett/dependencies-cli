# &#x1F53B;&#x1F53B;&#x1F53B;DEPRECATED: dependencies-cli&#x1F53B;&#x1F53B;&#x1F53B;

***
***This project has moved to [https://github.com/forcedotcom/dependencies-cli](https://github.com/forcedotcom/dependencies-cli)***.
***

Sample command line utilities around the [Salesforce Dependencies API](https://releasenotes.docs.salesforce.com/en-us/summer18/release-notes/rn_metadata_metadatacomponentdependency.htm). This API is currently in Pilot.

## Introduction : Dependency Grapher ##

![Graph](https://raw.githubusercontent.com/afawcett/dependencies-cli/master/img/example2.png)

This command produces [DOT formatted](https://www.graphviz.org/doc/info/lang.html) output for dependencies in an org allowing you visualize the dependencies in the org (see below for an example). 

You can pass flags to it to filter down the output further, since in most orgs the output can be quite dense. You can then paste the output from this command into [this website](http://viz-js.com/) to see the results or install locally on your desktop one of the following.

- [GraphViz Commandline](https://www.graphviz.org/download/)
- [VSCode Extension](https://marketplace.visualstudio.com/items?itemName=EFanZh.graphviz-preview)

## Setup and Use

**NOTE:** This command will in due course be published to NPM and thus unless you wish to contribute to the code for this plugin you will not need to perform the following steps. Meanwhile if you want to give it a go please feel free to install the command as follows.

1) Make sure you have the latest Salesforce CLI:

```
sfdx update
```

2) Install the plugin via npm

```
sfdx plugins:install dependencies-cli
```

3) Run the command:

```
sfdx dependency:components:report -u [alias|username]
```


## Rendering graph output locally

We document two options to visualize the produced graph locally:

1) Render the SVG as dependency graph in an image
2) Render the SVG as [d3-force](https://github.com/d3/d3-force) graph in JavaScript

### 1. Render the SVG as dependency graph in an image

- requires [Graphviz](http://graphviz.org/)

```
brew install graphviz
```

- produce the DOT graph file output

```
sfdx dependency:components:report -u [alias|username] -r dot  | tee graph.dot

```

- convert the DOT file to SVG

```
dot -T svg graph.dot > graph.svg
```

- open the SVG directly in your browser (Google Chrome works best)

```
open -a "Google Chrome" graph.svg
```

### 2. Render the SVG as [d3-force](https://github.com/d3/d3-force) graph in JavaScript

- requires [http-server](https://www.npmjs.com/package/http-server)

```
npm install http-server
```

- produce the graph in JSON format

```
sfdx dependency:components:report -u [alias|username] --json  | tee graph.json
```

- start the http server

```
http-server -a localhost -p 8000 &
```

- open the browser with [http://localhost:8000/index.html](http://localhost:8000/index.html) and select the produced JSON file to render

```
open -a "Google Chrome" http://localhost:8000
```

## Example Output

1) Raw DOT format output

```
digraph graphname {
  rankdir=RL;
  node[shape=Mrecord, bgcolor=black, fillcolor=lightblue, style=filled];
  // Nodes
  X00h11000000s7oIAAQ [label=<Case (Support) Layout<BR/><FONT POINT-SIZE="8">Layout</FONT>>]
  X00b11000000S28TAAS [label=<Up-sell / Cross-sell Opportunity<BR/><FONT POINT-SIZE="8">WebLink</FONT>>]
  X00h11000000s7oJAAQ [label=<Case Layout<BR/><FONT POINT-SIZE="8">Layout</FONT>>]
  X00h11000000s7oNAAQ [label=<Account (Marketing) Layout<BR/><FONT POINT-SIZE="8">Layout</FONT>>]
  X00b11000000S28SAAS [label=<Billing<BR/><FONT POINT-SIZE="8">WebLink</FONT>>]
  X00N11000002qGqQEAU [label=<Account.Contract<BR/><FONT POINT-SIZE="8">CustomField</FONT>>]
  X00N11000002q9aoEAA [label=<Account.formula1<BR/><FONT POINT-SIZE="8">CustomField</FONT>>]
  X00N11000002pkkvEAA [label=<Account.Red<BR/><FONT POINT-SIZE="8">CustomField</FONT>>]
  X00h11000000s7oOAAQ [label=<Account (Sales) Layout<BR/><FONT POINT-SIZE="8">Layout</FONT>>]
  X00h11000000s7oPAAQ [label=<Account (Support) Layout<BR/><FONT POINT-SIZE="8">Layout</FONT>>]
  X00h11000000s7oQAAQ [label=<Account Layout<BR/><FONT POINT-SIZE="8">Layout</FONT>>]
  X00h11000000s7oZAAQ [label=<Opportunity (Marketing) Layout<BR/><FONT POINT-SIZE="8">Layout</FONT>>]
  X00b11000000S28RAAS [label=<Delivery Status<BR/><FONT POINT-SIZE="8">WebLink</FONT>>]
  X00h11000000s7oaAAA [label=<Opportunity (Sales) Layout<BR/><FONT POINT-SIZE="8">Layout</FONT>>]
  X00h11000000s7obAAA [label=<Opportunity (Support) Layout<BR/><FONT POINT-SIZE="8">Layout</FONT>>]
  X00h11000000s7ocAAA [label=<Opportunity Layout<BR/><FONT POINT-SIZE="8">Layout</FONT>>]
  X00h11000000s7pfAAA [label=<Campaign Layout<BR/><FONT POINT-SIZE="8">Layout</FONT>>]
  X00b11000000S28QAAS [label=<View Campaign Influence Report<BR/><FONT POINT-SIZE="8">WebLink</FONT>>]
  X00h11000000s7phAAA [label=<Contract Layout<BR/><FONT POINT-SIZE="8">Layout</FONT>>]
  X00h11000000sB5RAAU [label=<CustomObject1 Layout<BR/><FONT POINT-SIZE="8">Layout</FONT>>]
  X00N11000002po9oEAA [label=<CustomObject1.Blue<BR/><FONT POINT-SIZE="8">CustomField</FONT>>]
  X03d110000006W4WAAU [label=<Contract.ContractRule<BR/><FONT POINT-SIZE="8">ValidationRule</FONT>>]
  X03d110000006W55AAE [label=<CustomObject1.IsBLueToo<BR/><FONT POINT-SIZE="8">ValidationRule</FONT>>]
  X03d110000006W50AAE [label=<Account.IsBLue<BR/><FONT POINT-SIZE="8">ValidationRule</FONT>>]
  X01I110000003zvLEAQ [label=<CustomObject1<BR/><FONT POINT-SIZE="8">CustomObject</FONT>>]
  // Paths
  X00h11000000s7oIAAQ->X00b11000000S28TAAS
  X00h11000000s7oJAAQ->X00b11000000S28TAAS
  X00h11000000s7oNAAQ->X00b11000000S28SAAS
  X00h11000000s7oNAAQ->X00N11000002qGqQEAU
  X00h11000000s7oNAAQ->X00N11000002q9aoEAA
  X00h11000000s7oNAAQ->X00N11000002pkkvEAA
  X00h11000000s7oOAAQ->X00N11000002q9aoEAA
  X00h11000000s7oOAAQ->X00N11000002pkkvEAA
  X00h11000000s7oOAAQ->X00N11000002qGqQEAU
  X00h11000000s7oOAAQ->X00b11000000S28SAAS
  X00h11000000s7oPAAQ->X00N11000002pkkvEAA
  X00h11000000s7oPAAQ->X00b11000000S28SAAS
  X00h11000000s7oPAAQ->X00N11000002qGqQEAU
  X00h11000000s7oPAAQ->X00N11000002q9aoEAA
  X00h11000000s7oQAAQ->X00b11000000S28SAAS
  X00h11000000s7oQAAQ->X00N11000002pkkvEAA
  X00h11000000s7oQAAQ->X00N11000002qGqQEAU
  X00h11000000s7oQAAQ->X00N11000002q9aoEAA
  X00h11000000s7oZAAQ->X00b11000000S28RAAS
  X00h11000000s7oaAAA->X00b11000000S28RAAS
  X00h11000000s7obAAA->X00b11000000S28RAAS
  X00h11000000s7ocAAA->X00b11000000S28RAAS
  X00h11000000s7pfAAA->X00b11000000S28QAAS
  X00h11000000s7phAAA->X00N11000002qGqQEAU
  X00h11000000sB5RAAU->X00N11000002po9oEAA
  X03d110000006W4WAAU->X00N11000002pkkvEAA
  X03d110000006W55AAE->X00N11000002po9oEAA
  X03d110000006W50AAE->X00N11000002po9oEAA
  X03d110000006W50AAE->X01I110000003zvLEAQ
  X00N11000002q9aoEAA->X00N11000002pkkvEAA
}
```


2) SVG dependency graph output

![Graph](./img/example2.png)

3) D3 force graph output

![Graph](./img/example3.png)
