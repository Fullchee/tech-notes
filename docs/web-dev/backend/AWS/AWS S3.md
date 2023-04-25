## Why S3

Blob storage

Like a giant hard drive in the cloud

For data you don't need to be able to access right away, see [AWS Glacier](https://aws.amazon.com/s3/storage-classes/glacier/)

## `cp`

```bash
aws s3 cp "<s3://url>" "local_destination_path"
```

Copy it to the Desktop with the same name as in S3

```bash
s3-cp() {
   if [ -z "$1" ] ; then
       echo 'Usage: s3-cp <s3://_url>'
       return
   fi
   aws s3 cp "$1" "$HOME/Desktop/$(basename $1)"
}
```

## `aws s3 presign`

-   it makes your file publicly available for anyone with the URL
-   I'm not sure why you'd do this?

## Sync

Copy from one S3 bucket to another

-   prod to staging

```bash
aws s3 sync s3://DOC-EXAMPLE-BUCKET-SOURCE s3://DOC-EXAMPLE-BUCKET-TARGET
```
