---
title: "View and Filter Data"
linkTitle: "View Data"
weight: 38
type: "docs"
tags: ["data management", "cloud", "sync"]
# SME: Aaron Casas
---

After the Data Management Service synchronizes the uploaded data in Viam, you can view it on the [**DATA** page in the Viam cloud](https://app.viam.com/data/view).

![Images, files, and sensors tabs](../img/tabs.png)

The **DATA** page shows data about:

- **Images**: PNG or JPEG files
- **Files**: binary data like point cloud data
- **Sensors**: tabular sensor counts (like gantry position)

If you click on an image or a file, a **Details** panel appears on the right with capture metadata.

![Data view with an image selected](../img/data_view.png)

## Filter Data

On the [**DATA** page in the Viam app](https://app.viam.com/data/view), you can filter data in the left **Filtering** panel.

For example, if you specify `Rover Rental` for location and click **SEARCH**, you can see all data captured on robots that belong to your `Rover Rental` location.

## Delete Data

You can delete image or file data from the [Viam app](https://app.viam.com).
To delete image data, click on an image in the **Images** subtab and click on **DELETE SELECTED**.
To delete a file, click on the file  in the **Files** subtab and click the **Delete** icon.

To delete all image, file, or sensor data respectively, click on **DELETE ALL** in the top right corner.

![Data view with no image selected showing the Delete all button](../img/delete_all.png)

You can also delete data using the [Viam CLI](../../cli/).

## Next Steps

To export your captured data from the cloud, see [Export Data](../export/).

You can use cloud image data to [train machine learning models](../../ml/train-model/) within Viam.

For a comprehensive tutorial on data management, see [Intro to Data Management](../../../tutorials/services/data-management-tutorial/).
