---
slug: common-batch-tasks
sidebar_position: 4
---

# Examples of Common Batch Operations

## Upload the Same File to All Records in a Project

```bash
cocli record list | grep -v 'ID' | cut -d ' ' -f1 | xargs -I {} cocli record upload {} ./FILE_FLAG
```

![cocli-upload-file-to-all-records](./img/cocli-upload-file-to-all-records.png)

## Create a Record for Each Folder in the Current Directory and Upload Files

Assume we have the following 5 folders, each containing several random files and folders, as shown in the structure below.

![list-folders-tree-view](./img/list-folders-tree-view.png)

We can use the Coscene CLI tool and standard Linux command line tools to create records and upload files all at once.

```bash
# Iterate through all subdirectories in the current directory
for dir in */; do
  # Remove the trailing slash from the directory name and create a new record, getting the record ID
  record_id=$(cocli record create -t "${dir%/}" | head -n1 | cut -d " " -f3)

  # Upload the contents of the current subdirectory to the created record
  cocli record upload -R "$record_id" "$dir"
done
```

![cocli-create-and-upload-multiple-folders](./img/cocli-create-and-upload-multiple-folders.png)

Open any record on the web interface to see that the command line has uploaded all files and folders from the local directory to the corresponding record.

![cocli-multiple-folders-uploaded](./img/cocli-multiple-folders-uploaded.png)

## Iterate Through All Records and Perform Operations

A common command line operation pattern is to iterate through all records in a user-specified project and perform operations based on a specific pattern.

```bash
# Get the list of all records in the project, iterate through and provide the Record ID for subsequent operations
for id in $(cocli record list | grep -v 'ID' | cut -d ' ' -f1); do
    # Use $id for subsequent batch operations
done
```

This pattern can be extended to connect more complex batch operations.

### Find All Empty Records Without Any Files

```bash
for id in $(cocli record list | grep -v 'ID' | cut -d ' ' -f1); do
    # Get the list of files in the record, removing the header
    files=$(cocli record list-files $id | tail -n +2)

    # Check if the file list is empty
    if [[ -z "$files" ]]; then
        # If the file list is empty, output the record ID
        echo "Record $id has no files."
    fi
done
```

### Tag All Empty Records

```bash
for id in $(cocli record list | grep -v 'ID' | cut -d ' ' -f1); do
    # Get the list of files in the record, removing the header
    files=$(cocli record list-files $id | tail -n +2)

    # Check if the file list is empty
    if [[ -z "$files" ]]; then
        # Tag all empty records with empty-record
        cocli record update $id -l empty-record
    fi
done
```

### Delete All Empty Records

:::danger
Please be very careful with the `delete` operation, as it may delete important data!!
:::

```bash
for id in $(cocli record list | grep -v 'ID' | cut -d ' ' -f1); do
    # Get the list of files in the record, removing the header
    files=$(cocli record list-files $id | tail -n +2)

    # Check if the file list is empty
    if [[ -z "$files" ]]; then
        # Delete the current record, using the -f flag to skip manual confirmation
        cocli record delete $id -f
    fi
done
```
