# Notes on using Amazon Web Services (AWS)

- [CloudWatch](#cloudwatch)
  * [Saving dashboard widgets](#saving-dashboard-widgets)
  * [A quick intrusion evidence filter](#a-quick-intrusion-evidence-filter)

<TOC>

## CloudWatch

### Saving dashboard widgets

You know what stinks? When you spend time creating a new dashboard widget and
you get it right, then you add it to a dashboard, and it shows up great. Then
you start doing something else, since you're used to the way modern web apps
auto-save. And you come back in a few hours to refresh your CloudWatch session
and find that your dashboard hasn't been saved, and the widget is gone. Time to
write it again.

So remember to save the dashboard when you add a widget. I assume this will be
fixed in a future version of CloudWatch.


### A quick intrusion evidence filter

[This gist](https://gist.github.com/andypayne/4141556e36ef833ff80d740bd9786236.js") shows a quick way:

```
fields @timestamp, @message
| filter @message like /(?i)(\/etc\/passwd)|(\<script\>alert)/
| sort @timestamp desc
| stats count() by bin(60s)
```

