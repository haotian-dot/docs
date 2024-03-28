---
sidebar_position: 3
---

# Automation

coScene's workflow is a task-based workflow system. As one of the three core engines of coScene, the flexible and powerful workflow system brings more possibilities to the data stored on the coScene platform. This article introduces the basic features of the workflow. For details on the workflow's usage and components, please refer to the workflow section in the operation guide.

## Seamless Integration with the Data Engine

The vast amount of data in the AI era brings endless possibilities, but it also poses challenges in data processing and application. In the actual production process, AI engineers need to go through a series of tasks such as data cleaning, preprocessing, training, testing, and deployment. These tasks require substantial human effort and time and are often repetitive. According to IBM research, AI engineers spend 80% of their time on data cleaning and preprocessing, rather than on AI model training. This phenomenon is more pronounced in companies without a solid data infrastructure.

coScene's workflow system is built upon coScene's data engine. Users no longer need to start from scratch to build data processing workflows. Instead, they can create data processing workflows on the coScene platform and invoke them within the workflow. In this way, users can focus more on AI model training rather than data cleaning and preprocessing.

Users can freely search, filter, organize, and consolidate data on coScene's data engine and then use these data search criteria as input for the workflow. The workflow can then automatically retrieve data from coScene's data engine based on user criteria and process it accordingly.

## Flexible Templates

coScene's workflow system offers a wealth of templates and a flexible custom DSL. Even engineers without cloud-native experience can easily modify and customize coScene's workflow templates, quickly constructing their workflows.

The DSL uses a YAML definition method and is compatible with custom Docker Image inputs and direct scripting, making it easy to convert one's workflow to coScene's.

## Easily Achieve Large-scale Scheduling

coScene fully embraces cloud-native, leveraging the flexibility of cloud-based scheduling and on-demand scaling to provide users with efficient, precise, and non-wasteful large-scale scheduling capabilities. If you choose coScene's SaaS product, coScene will automatically allocate computing resources based on your payment tier. If you opt for coScene's private deployment product, you can add any number of computing nodes to the coScene network and schedule computing tasks to these nodes as needed.

## Comprehensive API Interface

coScene provides a rich set of API interfaces to help you build automated workflows. You can use the API to create workflows, start workflows, check the status of a workflow, retrieve logs, obtain execution results, and more. By using the API, you can integrate coScene's workflow into your existing CI/CD or other internal processes. Want to run a large-scale regression test before merging code? Want to use scheduled tasks to automatically send newly uploaded data to an annotation company every day? No problem!

For detailed information about the API, please refer to our [API documentation].

## Powerful Observability

coScene's platform integrates all the statuses and metrics you need to monitor when using the workflow system. You can easily observe your workflow's execution status, results, logs, data sources, execution time, computing resources, and other user-concerned indicators and data on coScene's website. This information will also be returned in coScene's API, allowing you to retrieve it and integrate it into your automated processes.

## Notification System

Long-running workflows may encounter exceptions. coScene offers a notification system to help you detect anomalies in real-time and address them. You can easily configure notification rules on coScene's website. If a workflow encounters an exception, coScene will automatically notify users about the workflow's status through the configured channels.

The notification system also applies to events where the workflow **runs successfully**, **times out**, or faces **resource** limitations. For events that might occur in the workflow, please refer to the [workflow-related API documentation].

## References

1. https://www.wsj.com/articles/data-challenges-are-halting-ai-projects-ibm-executive-says-11559035800
