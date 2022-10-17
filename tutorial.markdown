---
layout: page
title: Tutorial
permalink: /tutorial/
---

### Demo Video

This video demonstrates the complete process of using Matcha to generate the data safety label in CSV format for an example app.

<div style="padding-bottom:56.25%; position:relative; display:block; width: 100%">
  <iframe width="100%" height="100%" src="https://www.youtube-nocookie.com/embed/q_yWhXEG0fc"
    frameborder="0" allow="autoplay; encrypted-media" allowfullscreen style="position:absolute; top:0; left: 0">
  </iframe>
</div>

<br>
### FAQ

#### Why no incomplete tasks are shown for my projects?
> There are three possible causes.
> - First, it could be that Matcha really can't detect any data access or transmission API calls or third-party libraries that collect/share data in your app. In this situation, we recommend you to use the keyword-based detection (Step 2 and 4) to double check.
> - Second, (which is the more common case), Matcha could not analyze your project because the indexing hasn't completed when the code analysis was conducted. To fix this issue, you just need to reopen the project after it has completed the indexing for at least once.
> - Third, If your app-level gradle file is not stored under the `app` folder, Matcha may not be able to detect it automatically and therefore cannot detect any third-party libraries. To fix this issue, you can manually open the corresponding gradle file to force Matcha to analyze it. 

#### Why can't I annotate variables that access UI elements via view binding?
> This is a known issue that we are still working on a fix for. The problem is that Java annotations can only be added where a Java variable/method/class etc. is defined, while view binding defines the view in an XML layout file which can't be annotated. A temporary fix is to add a dummy variable next to the detected API call, and add an annotation to the dummy variable using quickfixes. You can refer to the process of adding annotations in Step 2 and 4 in the demo video. This won't resolve the errors in the incomplete tasks list, but it can make sure the data practices related to these API calls are still counted when generating the data safety label.
