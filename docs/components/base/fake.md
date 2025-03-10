---
title: "Configure a Fake Base"
linkTitle: "fake"
weight: 20
type: "docs"
description: "Configure a fake base to use for testing without physical hardware."
images: ["/components/img/components/base.svg"]
tags: ["base", "components"]
# SMEs: Steve B
---

You can use a `fake` base to test implementing a base component on your robot without any physical hardware.

Configure a `fake` base as follows:

{{< tabs name="Configure a Fake Base" >}}
{{% tab name="Config Builder" %}}

Navigate to the **Config** tab of your robot's page in [the Viam app](https://app.viam.com).
Click on the **Components** subtab and navigate to the **Create component** menu.
Enter a name for your base, select the type `base`, and select the `fake` model.

Click **Create component**.

![An example configuration for a fake base in the Viam app Config Builder.](../img/fake-base-ui-config.png)

{{% /tab %}}
{{% tab name="JSON Template" %}}

```json {class="line-numbers linkable-line-numbers"}
{
    "name": "<your-base-name>",
    "type": "base",
    "model": "fake",
    "attributes": {}
}
```

{{% /tab %}}
{{< /tabs >}}

No attributes are available for `fake` bases.
See [GitHub](https://github.com/viamrobotics/rdk/blob/main/components/base/fake/base.go) for API call return specifications.
