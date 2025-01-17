## Basic Structure

A lifecycle configuration is specified as XML and consists of one or more lifecycle rules. The structure is as follows:

```xml
<LifecycleConfiguration>
	<Rule>
		<ID>**your lifecycle name**</ID>
        <Status>Enabled</Status>
        <Filter>
            <And>
            	<Prefix>projectA/</Prefix>
                <Tag>
                	<Key>key1</Key>
                    <Value>value1</Value>
                </Tag>
            </And>
        </Filter>
        **transition/expiration actions**
	</Rule>
	<Rule>
		...
	</Rule>
</LifecycleConfiguration>
```

Each rule contains the following:

- ID (optional): Indicates the content of the rule and is customizable.
- Status: Indicates whether the rule is enabled or disabled.
- Filter: Identifies objects to which the rule applies.
- Action: Actions that need to be performed on objects that match the above description.
- Time: `Days` (calculated based on the object's last modified date) or `Date` based on which actions are performed on objects.

## Rule Description

### Filter element

#### For all objects in a bucket

You can specify an empty filter, in which case the rule applies to all objects in the bucket.

```xml
<LifecycleConfiguration>
    <Rule>
        <Filter>
        </Filter>
        <Status>Enabled</Status>
        **transition/expiration actions**
    </Rule>
</LifecycleConfiguration>
```

#### Based on object key prefixes

Specify a prefix-based filter so that a rule applies only to objects with specific prefixes. For example, you can filter out objects based on the prefix `logs/`:

```xml
<LifecycleConfiguration>
    <Rule>
        <Filter>
           <Prefix>logs/</Prefix>
        </Filter>
        <Status>Enabled</Status>
        **transition/expiration actions**
    </Rule>
</LifecycleConfiguration>
```

#### Based on object tags

Specify a filter based on `key` and `value` so that a rule applies only to objects with the specific tag. For example, you can filter out objects based on tags `key=type` and `value=image`:
```xml
<LifecycleConfiguration>
    <Rule>
        <Filter>
           <Tag>
              <Key>type</Key>
              <Value>image</Value>
           </Tag>
        </Filter>
        <Status>Enabled</Status>
        **transition/expiration actions**
    </Rule>
</LifecycleConfiguration>
```

#### Use multiple filters

In COS, you can combine multiple filters using `AND`. For example, you can filter out objects based on the prefix `logs/` as well as tags `key=type` and `value=image`:
```xml
<LifecycleConfiguration>
    <Rule>
        <Filter>
            <And>
            	<Prefix>logs/</Prefix>
                <Tag>
              		<Key>type</Key>
              		<Value>image</Value>
           	 </Tag>
            </And>
        </Filter>
        <Status>Enabled</Status>
        **transition/expiration actions**
    </Rule>
</LifecycleConfiguration>
```

### Elements to describe actions

You can specify one or more predefined actions in a lifecycle rule so that these actions are performed when any objects meet the rule.

#### Transition action

Specify the Transition action to transition objects from one storage class to another. For a versioning-enabled bucket, the Transition action applies to the current object version. You can set the transition date to as short as 0 days. For example, transition objects to ARCHIVE storage after 30 days:

```xml
<Transition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</Transition>
```

#### Deletion after expiration

Specify the Expiration action to delete expired objects. For a versioning-disabled bucket, expired objects will be permanently deleted. For a versioning-enabled bucket, expired objects are **added with DeleteMarker** and become the current version. For example, delete objects with an expiration of 30 days:
```xml
<Expiration>
	<Days>30</Days>
</Expiration>
```

#### Incomplete Multipart Upload

Specify the AbortIncompleteMultipartUpload action to delete multipart upload tasks with specific UploadId if they are not successfully completed within the predefined time period. In this case, these tasks also cannot be resumed or indexed. For example, abort multipart upload tasks not successfully completed within 7 days:
```xml
<AbortIncompleteMultipartUpload>
	<Days>7</Days>
</AbortIncompleteMultipartUpload>
```

#### Objects of non-current versions

In a versioning-enabled bucket, the Transition action only applies to objects of the latest version and the Expiration action only results in adding delete markers to the objects. Therefore, COS provides the following actions to objects of non-current version:

Specify the NoncurrentVersionTransition action to transition the current version of objects to another storage class at a specified time. For example, transition the non-current versions of objects to ARCHIVE  storage after 30 days:

```xml
<NoncurrentVersionTransition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</NoncurrentVersionTransition>
```

Specify the NoncurrentVersionExpiration action to delete the current version of objects expired at a specified time. For example, delete the non-current versions of objects expired after 30 days:
```xml
<NoncurrentVersionExpiration>
	<Days>30</Days>
</NoncurrentVersionExpiration>
```

Specify the ExpiredObjectDeleteMarker action to clear the remaining delete markers. You can set it to `true` or `false`. This action is triggered by the NoncurrentVersionExpiration action (deleting expired historical versions). If ExpiredObjectDeleteMarker is enabled, when lifecycle execution deletes the last historical version in the lifecycle of an object, COS automatically deletes the remaining delete markers.

The details are as follows. If the NoncurrentVersionExpiration action (deleting expired historical versions) is in effect:
- If there is only one delete marker left, COS automatically deletes the last delete marker regardless of whether ExpiredObjectDeleteMarker is enabled.
- If there are multiple delete markers left, COS checks whether ExpiredObjectDeleteMarker is enabled. If `ExpiredObjectDeleteMarker` is `true`, COS automatically deletes the remaining delete markers. If `ExpiredObjectDeleteMarker` is `false`, COS does not delete the remaining delete markers.


```xml
<ExpiredObjectDeleteMarker>
	<Days>true|false</Days>
</ExpiredObjectDeleteMarker>
```

### Time element

#### Based on number of days

`Days` refers to the number of days since an object was last modified.
- For example, if an object is set to be transitioned to ARCHIVE storage after 0 days, when the object is uploaded at 2018-01-01 23:55:00 GMT+8, it will be added to the transition queue at 2018-01-02 00:00:00 GMT+8 and transitioned before 2018-01-02 23:59:59 GMT+8.
- For example, if an object is set to be deleted after 1 day due to expiration, when the object is uploaded at 2018-01-01 23:55:00 GMT+8, it will be added to the expiration queue at 2018-01-03 00:00:00 GMT+8 and deleted before 2018-01-03 23:59:59 GMT+8.

#### Based on a specific date

Perform the predefined action on all qualified objects based on the filter criteria at the specific `Date`. The date value must conform to the ISO 8601 format. The time is always 00:00 GMT+8.
For example, use `2018-01-01T00:00:00+08:00` for January 1, 2018.


