---
layout: post
title:  "How to monitor application using probes in OpenShift?"
date:   2020-04-22
categories: [openshift, nodejs]
---

<!-- ![How to monitor application using probes in OpenShift?](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/6.png) -->

### Objective
- Add Readiness Probe to `nodejs` Application
- Add Liveness Probe to `nodejs` Application

**Step 1:** Deploy `nodejs` application using `S2I`.
Refer [How to deploy application using Source to Image (S2I) in OpenShift?](https://developersthought.in/openshift/nodejs/2020/04/15/application-deployment-s2i.html) blog.

**Step 2:**  Open Dashobard

![Step 2](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_1.JPG)

**Step 3:**  Login with developer user

![Step 3](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_2.jfif)

**Step 4:**  Go to project my-project

![Step 4](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_3.JPG)

**Step 5:**  Go to application nodejs

![Step 5](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_4.JPG)

**Step 6:**  Go to deployment

![Step 6](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_5.JPG)

**Step 7:**  Go to health checks

![Step 7](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_6.JPG)

**Step 8:**  Add readiness probe

![Step 8](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_7.JPG)

**Step 9:**  Add liveness probe & save

![Step 9](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_8.JPG)

### Show Your Support

- [Buy me a coffee](https://www.buymeacoffee.com/sagarjadhv23) If you like the content and find it useful.
- Report an issue [here](https://github.com/developersthought/roadmap/issues/new) If you find a bug or want to improve the content.