---
layout: page
title: Tutorial
permalink: /tutorial/
---

### Demo Video

This video demonstrates the complete process of using Matcha to generate the data safety label in CSV format for an example app. Matcha breaks down this process to five steps, and your goal is just to complete all the tasks by adding annotations and modifying an auto-generated XML config file.

<div style="padding-bottom:56.25%; position:relative; display:block; width: 100%">
  <iframe width="100%" height="100%" src="https://www.youtube-nocookie.com/embed/q_yWhXEG0fc"
    frameborder="0" allow="autoplay; encrypted-media" allowfullscreen style="position:absolute; top:0; left: 0">
  </iframe>
</div>

<br>

### How to add annotations to fill out data practices by your app

In [our recent research](https://dl.acm.org/doi/10.1145/3491102.3502012), we learned that developers' perceptions of the concept "data collection" and "sharing" often differ from the exact definitions of the app store. Therefore, Matcha doesn't directly ask you what data is collected or shared; instead, it detects API calls that access user data or transmit user data out of your app (e.g., sent out of the device, sent to another app), and asks you to add `@DataAccess` and `@DataTransmission` annotations to describe how the data is used. Matcha will automatically translate the access and transmission annotations to data collection and sharing practices in the data safety label, as shown in the following diagram:

![plugin installation screenshot](/assets/images/annotation-dsl-mapping.png)

Matcha provides quick-fixes to make it easy to add these annotations. You can see instructions on how to apply these quickfixes in the Matcha tutorial panel within the IDE, or check out the demo video for more details (see the Step 1, 2, 3, 4).

Using annotations allows you to provide really fine-grained information about your apps' data practices, which makes updating your data safety label easier. If you later modifies any data practices, you just need to modify/add/remove the corresponding annotations and then click the button to re-generate the CSV file.

### How to modify the XML config file to fill out data practices by libraries

The data collected or shared by third-party data practices also needs to be reported in your data safety label. To streamline this task, our plugin automatically detects SDKs integrated in your app, and helps you fill out the label based on the official guidance of the corresponding SDKs if available.

The use of third-party SDKs may cause two types of data practices. The first type is required data collection and sharing, i.e., the data will always be collected as long as you integrated the SDK to your app. Matcha handles this part of data practices automatically and you don't need to do anything about it.

The second type is optional data collection and sharing, i.e., whether the data is collected and shared depends on your usage of the SDK. Matcha generates an XML configuration file to allow you to customize your label based on how your app uses the SDK (`safety_section/library_safety_section_config_xml`). In this file, each `<data>` tag represents one optional data collection/sharing case and the enclosed text describes the applicable condition. You should either delete the data tag if doesn't apply to your SDK usage or keep it if otherwise. Finally, set the `verified` attribute to true for the SDK that you have finished reviewing. You can find more detailed examples in the demo video.

#### (If you're curious) How did we learn about the data practices of third-party SDKs?
Matcha supports all the SDKs listed on the [Google Play SDK Index](https://play.google.com/sdks) that also provide a link to their data safety disclosure guidance. All the SDKs that Matcha supports are summarized in this [json file](https://gist.github.com/i7mist/1fa774af300fe8639b4e615923b437f0). Note that some SDKs' official guidance on data safety disclosure may have incomplete or ambiguious information. If you find certain information in our json file inaccurate, please let us know and we'd be happy to fix it once the issue is confirmed.

### FAQ

#### Why no incomplete tasks are shown for my projects?
> There are three possible causes.
> - First, it could be that Matcha really can't detect any data access or transmission API calls or third-party libraries that collect/share data in your app. In this situation, we recommend you to use the keyword-based detection (Step 2 and 4) to double check if your app collects or shares any data.
> - Second, (which is the more common case), Matcha could not analyze your project because the indexing hasn't completed when the code analysis was conducted. To fix this issue, you just need to reopen the project after it has completed the indexing for at least once.
> - Third, If your app-level gradle file is not stored under the `app` folder, Matcha may not be able to detect it automatically and therefore cannot detect any third-party libraries. To fix this issue, you can manually open the corresponding gradle file to force Matcha to analyze it. 

#### Why can't I annotate variables that access UI elements via view binding?
> This is a known issue that we are still working on a fix for. The problem is that Java annotations can only be added where a Java variable/method/class etc. is defined, while view binding defines the view in an XML layout file which can't be annotated. A temporary fix is to add a dummy variable next to the detected API call, and add an annotation to the dummy variable using quickfixes. You can refer to the process of adding annotations in Step 2 and 4 in the demo video. This won't resolve the errors in the incomplete tasks list, but it can make sure the data practices related to these API calls are still counted when generating the data safety label.

If your problem is not solved, please create an [issue on GitHub](https://github.com/Matcha-IDE/Matcha-IDE/issues), or send an email to <tianshil@cs.cmu.edu>.
