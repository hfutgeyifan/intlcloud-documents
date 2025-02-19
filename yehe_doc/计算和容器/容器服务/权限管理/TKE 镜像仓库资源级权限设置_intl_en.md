## TCR Permissions Overview

The TCR address format is as follows: `ccr.ccs.tencentyun.com/${namespace}/${name}:${tag}`.
The following fields are required for configuring the permissions of an image repository:
- `${namespace}`: The namespace to which the image repository belongs.
- `${name}`: The name of the image repository.

>! Do not add slashes (/) to the namespace `${namespace}` and the image name `${name}`.
> The `${tag}` field currently is only for authenticating the permissions for deleting. For more information, see [Image Tag Permissions](#Tag).
> 
`${namespace}` and `${name}` fields allow you to develop detailed permission schemes for collaborators to flexibly manage access permissions.  
For example:
- Permit collaborator A to pull images
- Forbid collaborator A from deleting images
- Forbid collaborator B from pulling the images in the namespace ns1

If you do not need to manage the permissions of the image repository in detail, you can use [Preset Policy Authorization](#PresetPpolicyAuthorization).
If you need to manage the collaborator permissions in detail, please use [Custom Policy Authorization](#CustomPolicyAuthorization).
The TCR utilizes CAM (Cloud Access Management) to manage access permissions. You can learn more about how to use CAM here:
- [User management](https://intl.cloud.tencent.com/document/product/598/10599)
- [Policy management](https://intl.cloud.tencent.com/document/product/598/10601)
- [Authorization management](https://intl.cloud.tencent.com/document/product/598/10602)

[](id:PresetPpolicyAuthorization)
## Preset Policy Authorization

To simplify TCR permissions management, two preset policies are configured in TCR:
- [Full read-write access permissions for image registry (CCR)](https://console.cloud.tencent.com/cam/policy/detail/419082&QcloudCCRFullAccess&2)
This preset policy configures all permissions of TCR. If a collaborator is associated with this preset policy, he/she will have the same permissions of the image repository as the admin. For details, see [Authorizing by using custom policies](https://intl.cloud.tencent.com/document/product/457/37499).
- [Read-only access permission for image registry (CCR)](https://console.cloud.tencent.com/cam/policy/detail/419084&QcloudCCRReadOnlyAccess&2)
This preset policy includes only the read-only permission of TCR. If a collaborator is **only** associated with this policy in TCR, the following operations will be prohibited:
 - Push images with `docker push`
 - Create a namespace of image registry
 - Delete a namespace of image registry
 - Create an image repository
 - Delete an image repository
 - Delete an image tag

If you do not know how to associate a collaborator with a preset policy, please see [Policy](https://intl.cloud.tencent.com/document/product/598/10601) and [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

[](id:CustomPolicyAuthorization)
## Custom Policy Authorization

With a custom policy, you can associate different permissions with different collaborators.
Taking the following factors into account when assigning permissions:
- **Resource**: Which image repositories are associated with this permission policy, for example, all image repositories are described as `qcs::ccr:::repo/*`. For more information, see [CAM Resource Description Method](https://cloud.tencent.com/document/product/598/10606).
- **Action**: What operations, such as deleting and creating, this permission policy allows the collaborators to perform on the **resource**. The operations are usually described using APIs.
- **Effect**: The effect the permission policy has on the collaborator (Allow/Deny)

When you have planned the permission settings, you can assign the permissions. The following example shows how to "permit collaborators to create an image repository":
1. Create a custom policy as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
  1. Log in to the Tencent Cloud console using your developer account.
  2. Go to the [CAM custom policy management page](https://console.cloud.tencent.com/cam/policy/custom) and click **Create a custom policy** to open the "Select a policy creation method" dialog box, as shown in the following figure:
![Select a method to create policy](https://qcloudimg.tencent-cloud.cn/raw/a8d3d5f685c6064b57461b1e9ece4ad0.png)
 3. Select **Create by policy syntax** > **Blank template**.
![Select a template](https://qcloudimg.tencent-cloud.cn/raw/2ac6c17390f5f9302693327465a77be4.png)
 4. Click **Next** to go to the **Edit policy** page.
 5. Set the policy name and enter the following code to the “Edit policy content” edit box.
```
        {
            "version": "2.0",
            "statement": [{
                "action": "ccr:CreateRepository",
                "resource": "qcs::ccr:::repo/*",
                "effect": "allow"
            }]
        }
```
 For example, you can set the policy name `ccr-policy-demo`, as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/0c47647c5c72a8942548efc80b53fe32.png)

>? At the **end** of "resource", use \* to indicate that an image repository can be created under any namespace.
>
 6. Click **Create policy** to complete the process.
![](https://qcloudimg.tencent-cloud.cn/raw/c56ce37325cbb2a5cf2c7964cf9b5189.png)
2. Associate with the custom policy. You can associate the policy created in step 1 (ccr-policy-demo) to any collaborator. For details, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602). After the association, the collaborator can have **the permissions to create image repositories under any namespace**.
\_resource `qcs::ccr:::repo/*` Format description:
 - `qcs::ccr:::` is a fixed format, indicating the developer's TCR service.
 - `repo` is a fixed prefix, representing the resource type, which is an image repository here.
 - `*` after the slash (`/`) means matching all image repositories.

For a detailed description of resource, see [CAM Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606).

#### Authorizing by resource

You can grant permissions for multiple resources at a time. For example, to "permit the deletion of the image repositories in namespaces `foo` and `bar`", you can create the following custom policy:
```
{
    "version": "2.0",
    "statement": [{
        "action": [
            "ccr:BatchDeleteRepository",
            "ccr:DeleteRepository"
        ],
        "resource": [
            "qcs::ccr:::repo/foo/*",
            "qcs::ccr:::repo/bar/*"
        ],
        "effect": "allow"
    }]
}
```

>!
> - `foo/*` in `qcs::ccr:::repo/foo/*` means all images in the image repository namespace `foo`.
> - `bar/*` in `qcs::ccr:::repo/bar/*` means all images in the image repository namespace `bar`.

#### Authorizing by action (API)

You can configure multiple `actions` for a resource for a centralized management of resource permissions. For example, to "permit the creation, deletion and push of image repositories in the namespace `foo`", you can create the following custom policy:
```
{
    "version": "2.0",
    "statement": [{
        "action": [
            "ccr:CreateRepository",
            "ccr:BatchDeleteRepository",
            "ccr:DeleteRepository",
            "ccr:push"
        ],
        "resource": "qcs::ccr:::repo/foo/*",
        "effect": "allow"
    }]
}
```

## Permission List

#### docker client permissions

resource： `qcs::ccr:::repo/${namespace}/${name}`  
action:
- `ccr:pull`: Use the docker command line to pull an image
- `ccr:push`: Use the docker command line to push an image

#### Namespace permissions

resource: `qcs::ccr:::repo/${namespace}`  
action:

- `ccr:CreateCCRNamespace` Create an image repository namespace
- `ccr:DeleteUserNamespace` Delete an image repository namespace

Feature guide: ****TKE**** > ****Image Repositories**** in the left sidebar > ****My images**** > ****Namespace****.
![Create or delete permissions of an image repository namespace](https://qcloudimg.tencent-cloud.cn/raw/385be310dee81a4d2e727130062d0561.png)


#### Image repository permissions

resurce: `qcs::ccr:::repo/${namespace}/${name}`  
action:
- `ccr:CreateRepository` Create an image repository
- `ccr:DeleteRepository` Delete an image repository
- `ccr:BatchDeleteRepository` Batch delete image repositories
- `ccr:GetUserRepositoryList` View the list of image repositories

Feature guide: ****TKE**** > ****Image Repositories**** in the left sidebar > ****My images**** > ****My images****.
![Permissions of an image repository](https://qcloudimg.tencent-cloud.cn/raw/7c37984880a3385e31a1b410373e91f0.png)

>! To prevent a collaborator from deleting certain images, configure multiple actions.
>
For example, to prohibit deleting any image repository:
```
{
    "version": "2.0",
    "statement": [{
        "action": [
            "ccr:BatchDeleteRepository",
            "ccr:DeleteRepository"
        ],
        "resource": "qcs::ccr:::repo/*",
        "effect": "deny"
    }]
}
```

[](id:Tag)
#### Image tag permissions

resource: `qcs::ccr:::repo/${namespace}/${name}:${tag}`  
action： `ccr:DeleteTag` Delete image tag permissions

Feature guide: ****TKE**** > ****Image Repositories**** in the left sidebar > ****My images**** > ****My images**** > click an image name > ****Image tag**** page.
![Permissions of an image repository](https://qcloudimg.tencent-cloud.cn/raw/07482dfbea7d0cd8fcfe8a74902b1eec.png)





