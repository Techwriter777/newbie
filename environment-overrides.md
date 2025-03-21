# Environment Overrides

You can view all environments associated with an application under the **Environment Overrides** section.

![Figure 1: Environment Overrides Section](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/creating-application/environment-overrides/environment-override-v3.jpg)

The Environment Overrides section allows you to customize the **Deployment Template**, **ConfigMaps**, and **Secrets** for different environments such as development, testing, staging, and production.

## How it works

* When you add a deployment pipeline to an application's workflow, each environment configuration initially inherits the Deployment Template, ConfigMap and Secret from the **Base Configurations** of the application.
* The **Environment Overrides** section lets you customize those Deployment Template, ConfigMap and Secret per environment without affecting those of other environments. For example, in a non-production environment, you might allocate `100m` CPU, while in production, you may increase it to `500m` to handle higher traffic.

***

## Environment Configurations Page

{% hint style="warning" %}
#### Who Can Perform This Action?

Users need to have Admin role or above (along with access to the environment and applications) to perform environment override.
{% endhint %}

1.  In your application, go to **Configurations** → **Environment Overrides**.

    ![Figure 2: Accessing Environment Overrides](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/creating-application/environment-overrides/config-env-override.jpg)
2.  Select an environment whose configurations you wish to modify.

    ![Figure 3: Selecting Environment](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/creating-application/environment-overrides/environment-override-v3.jpg)
3.  You will get the following options (similar to the **Base Configurations** page):

    * [Deployment Template](broken-reference)
    * [ConfigMaps](broken-reference)
    * [Secrets](broken-reference)

    ![Figure 4: Configuration Options](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/creating-application/environment-overrides/env-config-screen.gif)

Let's visit each of the configuration files and see how to override their values for the selected environment (say _banking-final_).

***

## Override Deployment Template

As you can see, the Deployment Template for the _banking-final_ environment shows 3 tabs:

* Inherited
* No override or Override
* Dry run

1.  Go to the **Inherited** tab. This will show the inherited configuration in a read-only YAML editor. You cannot edit any values here.

    ![Figure 5: Inherited Deployment Template](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/creating-application/environment-overrides/inherited-dt.gif)
2.  Clicking **No override** to override the inherited configuration (if not done already).

    ![Figure 6: No Override Tab](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/creating-application/environment-overrides/no-override-tab.gif)
3.  Click the **Create Override** button.

    ![Figure 7: Creat Override Button](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/creating-application/environment-overrides/create-override.gif)
4. In the same tab (now labelled as **Override**), you can choose any one mode for changing the configuration values:
   * **YAML** - This mode has a YAML based editor intended for advanced users. Click here to know more about each key-value pair within the `YAML` section.
   * **GUI** - This mode has a user-friendly interface intended for beginner to advanced users. Click here to know more about each field within the `GUI` section.

{% hint style="info" %}
#### Note

Users who are not super-admins will land on GUI mode when they override; whereas super-admins will land on YAML mode. This is just the default behavior, users can still toggle the mode if needed.
{% endhint %}

Let's choose YAML mode for now and proceed. If you prefer GUI mode, go to [Override Deployment Template using GUI](broken-reference) section.

5. You can override the values using any merge strategy:
   * [Patch](broken-reference)
   * [Replace](broken-reference)

### Using Patch Strategy

* Only the fields you explicitly specify are updated.
* The patched template will continue to depend on the base configuration, so all other inherited fields remain unchanged and will continue to inherit in future.
* Best for minor edits.

| Field    | Inherited Configuration | Input (with Patch) | Final Configuration  |
| -------- | ----------------------- | ------------------ | -------------------- |
| cpu      | 100m                    | 500m               | 500m                 |
| memory   | 256Mi                   | _(Not specified)_  | 256Mi _(Unchanged)_  |
| replicas | 2                       | _(Not specified)_  | 2 _(Unchanged)_      |
| logLevel | "info"                  | _(Not specified)_  | "info" _(Unchanged)_ |
| timeout  | (Not specified)         | 30s                | 30s (Added)          |

You can achieve this by doing either of the following to achieve the same outcome:

* If you know the fields you wish to change, simply enter the changed key-value fields along with indentation (if any).

{% embed url="https://www.youtube.com/watch?v=phhv1_2eStI" %}

* Or you may copy-paste the entire config, and change the fields.

{% embed url="https://www.youtube.com/watch?v=4eHM5ZsNoCg" %}

### Using Replace Strategy

* The entire configuration is replaced with your new environment-specific settings.
* The replaced template will no longer depend or inherit from base configuration anymore.
* Best for a complete override.

| Field    | Inherited Configuration | Input (with Replace) | Final Configuration |
| -------- | ----------------------- | -------------------- | ------------------- |
| cpu      | 100m                    | 500m                 | 500m                |
| memory   | 256Mi                   | 512Mi                | 512Mi               |
| replicas | 2                       | _(Not specified)_    | _(Removed)_         |
| logLevel | "info"                  | _(Not specified)_    | _(Removed)_         |
| timeout  | (Not specified)         | 30s                  | 30s (Added)         |

![Figure 8: Replace Strategy for Deployment Template](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/creating-application/environment-overrides/replace-dt.gif)

{% embed url="https://www.youtube.com/watch?v=x-ABYU4y-c0" %}

{% hint style="info" %}
#### What if some keys are locked from editing?

You cannot modify locked keys in an environment's deployment template unless you are a super-admin. Refer Lock Deployment Configuration to know more.
{% endhint %}

***

## Override ConfigMap & Secret

If you want to configure your ConfigMap and Secret at the application-level then you can provide them in ConfigMaps and Secrets, but if you want to have environment-specific ConfigMap and Secret, use **Environment Override** to create them. At the time of deployment, it will pick both of them and pass them to your cluster.

The process to override both ConfigMaps and Secrets is similar to [Override Deployment Template](broken-reference). Refer the tutorials below to know the process in YAML mode. In case you wish to use GUI mode, skip to [Overriding in GUI mode](broken-reference).

### Patch Strategy

{% embed url="https://www.youtube.com/watch?v=kYE5iFctg4E" %}

{% hint style="info" %}
#### Impact of Patch strategy on Base Configuration's CM/Secret?

You cannot delete a ConfigMap or Secret in **Base Configurations** if you have used 'Patch' strategy for overridding ConfigMap or Secret at your environment-level. This happens because they are still dependent and inheriting their values from Base Configurations.
{% endhint %}

### Replace Strategy

{% embed url="https://www.youtube.com/watch?v=lSoj8wwOej0" %}

***

## Using GUI Mode for Overridding

The above sections, i.e., [Override Deployment Template](broken-reference) and [Override ConfigMap & Secret](broken-reference) explained the process of environment override using YAML.

Refer the below tutorial videos to know the process of overriding them using GUI.

### Override Deployment Template using GUI

{% embed url="https://www.youtube.com/watch?v=Wh5WKvkYNDw" %}

{% hint style="info" %}
#### Want to customize the deployment template values displayed on GUI? [![](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/elements/EnterpriseTag.svg)](https://devtron.ai/pricing)

The GUI mode shows limited number of fields as specified by the super-admin in the GUI schema. Refer Customize GUI to know more.
{% endhint %}

### Override ConfigMaps and Secrets using GUI

{% embed url="https://www.youtube.com/watch?v=UOTKLVuSkDg" %}

***

## Delete Override

This action will discard the current overrides and the base configuration file (in this example, deployment template) will be restored back for the environment.

1. On the right side, click the kebab menu (3 vertical dots).
2. Click **Delete Override**.
3. Confirm the deletion in the dialogbox.

![Figure 9: Delete Override Option](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/creating-application/environment-overrides/delete-override.gif)

***

## Protected Environment Configurations [![](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/elements/EnterpriseTag.svg)](https://devtron.ai/pricing)

Any changes made to the protected environment configurations (Deployment Template, ConfigMap, Secret) will require approval if an approval policy is enforced.

{% embed url="https://www.youtube.com/watch?v=_BidCVR3hxY" %}
