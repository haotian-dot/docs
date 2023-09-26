---
sidebar_position: 6
---

# Test Metadata and Test Results

> Understand how to customize the output test results, how to view the progress and run products of the batch test and the individual test in it, and how to play the shadow mode under the visualization interface to compare outputs, etc.

## Output Test Results

You can customize the output test results through configuration files and test codes, etc. Currently, it supports outputting parsable result files and output charts.

### Output Parsable Result Files

Batch testing supports parsing JUnit XML format result files. In the 'script' parameter of the configuration file, you can use the following command to create an XML format result file at `path`:

\```
pytest --junitxml=path
\```

For specific examples, please see [Configuration File Format and Sample - Output Test Result File](../8-regression/9-yaml-sample.md#output-test-result-file).

The JUnit XML format result file supported for parsing is as follows, where the result data to JUnit XML format mapping please refer to [JUnit Mapping](https://www.ibm.com/docs/en/developer-for-zos/14.1?topic=formats-junit-xml-format#junitschema__table_junitmap):

\```
... (the XML content)
\```

### Output Charts

You can add custom attributes starting with "cos\_" in the test report, such as `cos_customer_name`. These custom attributes will be uploaded to CoScene along with the default metrics. CoScene will collect and analyze these custom attributes, and group, sort, and filter the metrics based on them.

You can use custom chart names starting with "cos\_" in the test code file in the image to output charts in the test results, with the following format:

\```
... (the python code)
\```

### Output Shadow Mode Files

> Output files to the specified directory as test output. The .bag files in it can be played in comparison with the files in the original record on the visualization interface.

You can use the command in the 'script' field of the configuration file to output the file to the `/cos/outputs` directory as a test output. For specific examples, please see [Configuration File Format and Sample - Output Shadow Mode Files](../8-regression/9-yaml-sample.md#output-shadow-mode-files).

The test output will be displayed in the "Test Output" column of the test details page, displayed hierarchically according to the corresponding test suite and record.

![result-12](../img/shadow-mode-1.png)

<br />

## View Running Progress and Products

1. The list on the batch test page displays the batch tests run in the project and information. You can click on a batch test number to view its details page:

   ![result-1](../img/status-1.png)

... (the rest of the content)
