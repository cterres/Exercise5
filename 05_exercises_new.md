---
title: 'Weekly Exercises #5'
author: "Cat Terres"
output: 
  html_document:
    keep_md: TRUE
    toc: TRUE
    toc_float: TRUE
    df_print: paged
    code_download: true
---





```r
library(tidyverse)     # for data cleaning and plotting
library(gardenR)       # for Lisa's garden data
library(lubridate)     # for date manipulation
library(openintro)     # for the abbr2state() function
library(palmerpenguins)# for Palmer penguin data
library(maps)          # for map data
library(ggmap)         # for mapping points on maps
library(gplots)        # for col2hex() function
library(RColorBrewer)  # for color palettes
library(sf)            # for working with spatial data
library(leaflet)       # for highly customizable mapping
library(ggthemes)      # for more themes (including theme_map())
library(plotly)        # for the ggplotly() - basic interactivity
library(gganimate)     # for adding animation layers to ggplots
library(transformr)    # for "tweening" (gganimate)
library(gifski)        # need the library for creating gifs but don't need to load each time
library(shiny)         # for creating interactive apps
theme_set(theme_minimal())
```


```r
# SNCF Train data
small_trains <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-02-26/small_trains.csv") 

# Lisa's garden data
data(garden_harvest)

# Lisa's Mallorca cycling data
mallorca_bike_day7 <- read_csv("https://www.dropbox.com/s/zc6jan4ltmjtvy0/mallorca_bike_day7.csv?dl=1") %>% 
  select(1:4, speed)

# Heather Lendway's Ironman 70.3 Pan Am championships Panama data
panama_swim <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_swim_20160131.csv")

panama_bike <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_bike_20160131.csv")

panama_run <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_run_20160131.csv")

#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
```

## Put your homework on GitHub!

Go [here](https://github.com/llendway/github_for_collaboration/blob/master/github_for_collaboration.md) or to previous homework to remind yourself how to get set up. 

Once your repository is created, you should always open your **project** rather than just opening an .Rmd file. You can do that by either clicking on the .Rproj file in your repository folder on your computer. Or, by going to the upper right hand corner in R Studio and clicking the arrow next to where it says Project: (None). You should see your project come up in that list if you've used it recently. You could also go to File --> Open Project and navigate to your .Rproj file. 

## Instructions

* Put your name at the top of the document. 

* **For ALL graphs, you should include appropriate labels and alt text.** 

* Feel free to change the default theme, which I currently have set to `theme_minimal()`. 

* Use good coding practice. Read the short sections on good code with [pipes](https://style.tidyverse.org/pipes.html) and [ggplot2](https://style.tidyverse.org/ggplot2.html). **This is part of your grade!**

* **NEW!!** With animated graphs, add `eval=FALSE` to the code chunk that creates the animation and saves it using `anim_save()`. Add another code chunk to reread the gif back into the file. See the [tutorial](https://animation-and-interactivity-in-r.netlify.app/) for help. 

* When you are finished with ALL the exercises, uncomment the options at the top so your document looks nicer. Don't do it before then, or else you might miss some important warnings and messages.

## Warm-up exercises from tutorial

  1. Choose 2 graphs you have created for ANY assignment in this class and add interactivity using the `ggplotly()` function.


```{=html}
<div id="htmlwidget-3d473754d8aca1455cd9" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-3d473754d8aca1455cd9">{"x":{"data":[{"orientation":"v","width":0.900000000001455,"base":0,"x":[18451],"y":[181],"text":"date: 2020-07-08<br />weight:  181<br />date: 18451","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(19,43,67,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18452],"y":[78],"text":"date: 2020-07-09<br />weight:   78<br />date: 18452","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(20,45,70,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18455],"y":[130],"text":"date: 2020-07-12<br />weight:  130<br />date: 18455","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(24,53,80,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18456],"y":[47],"text":"date: 2020-07-13<br />weight:   47<br />date: 18456","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(25,55,84,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18457],"y":[152],"text":"date: 2020-07-14<br />weight:  152<br />date: 18457","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(27,58,87,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18458],"y":[1057],"text":"date: 2020-07-15<br />weight: 1057<br />date: 18458","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(28,60,91,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18460],"y":[347],"text":"date: 2020-07-17<br />weight:  347<br />date: 18460","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(30,66,97,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18461],"y":[294],"text":"date: 2020-07-18<br />weight:  294<br />date: 18461","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(32,68,101,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18462],"y":[531],"text":"date: 2020-07-19<br />weight:  531<br />date: 18462","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(33,71,104,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18463],"y":[179],"text":"date: 2020-07-20<br />weight:  179<br />date: 18463","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(34,73,108,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18465],"y":[655],"text":"date: 2020-07-22<br />weight:  655<br />date: 18465","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(37,79,115,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18467],"y":[525],"text":"date: 2020-07-24<br />weight:  525<br />date: 18467","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(40,84,122,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18468],"y":[901],"text":"date: 2020-07-25<br />weight:  901<br />date: 18468","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(41,87,126,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18470],"y":[785],"text":"date: 2020-07-27<br />weight:  785<br />date: 18470","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(44,92,133,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18471],"y":[76],"text":"date: 2020-07-28<br />weight:   76<br />date: 18471","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(45,95,137,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18472],"y":[514],"text":"date: 2020-07-29<br />weight:  514<br />date: 18472","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(47,98,141,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18473],"y":[626],"text":"date: 2020-07-30<br />weight:  626<br />date: 18473","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(48,101,144,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18474],"y":[174],"text":"date: 2020-07-31<br />weight:  174<br />date: 18474","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(49,103,148,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18475],"y":[1130],"text":"date: 2020-08-01<br />weight: 1130<br />date: 18475","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(51,106,152,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18477],"y":[1155],"text":"date: 2020-08-03<br />weight: 1155<br />date: 18477","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(54,112,160,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18480],"y":[127],"text":"date: 2020-08-06<br />weight:  127<br />date: 18480","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(58,120,171,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18481],"y":[1327],"text":"date: 2020-08-07<br />weight: 1327<br />date: 18481","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(59,123,175,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18482],"y":[1697],"text":"date: 2020-08-08<br />weight: 1697<br />date: 18482","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(61,126,179,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18485],"y":[1029],"text":"date: 2020-08-11<br />weight: 1029<br />date: 18485","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(65,135,191,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18487],"y":[599],"text":"date: 2020-08-13<br />weight:  599<br />date: 18487","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(68,141,198,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18489],"y":[351],"text":"date: 2020-08-15<br />weight:  351<br />date: 18489","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(71,147,206,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[0.900000000001455,0.900000000001455],"base":[0,2888],"x":[18492,18492],"y":[2888,233],"text":["date: 2020-08-18<br />weight: 2888<br />date: 18492","date: 2020-08-18<br />weight:  233<br />date: 18492"],"type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(75,156,218,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18494],"y":[70],"text":"date: 2020-08-20<br />weight:   70<br />date: 18494","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(78,162,227,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18495],"y":[997],"text":"date: 2020-08-21<br />weight:  997<br />date: 18495","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(80,165,231,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18497],"y":[747],"text":"date: 2020-08-23<br />weight:  747<br />date: 18497","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(83,171,239,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18499],"y":[179],"text":"date: 2020-08-25<br />weight:  179<br />date: 18499","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(86,177,247,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[18449],"y":[0],"name":"99_edca43bfa051b21ae50dd5bd9d8ffca9","type":"scatter","mode":"markers","opacity":0,"hoverinfo":"skip","showlegend":false,"marker":{"color":[0,1],"colorscale":[[0,"#132B43"],[0.00334448160538159,"#132B44"],[0.00668896321068739,"#132C44"],[0.010033444816069,"#142C45"],[0.0133779264213748,"#142D45"],[0.0167224080267564,"#142D46"],[0.0200668896321379,"#142D46"],[0.0234113712374437,"#142E47"],[0.0267558528428253,"#152E47"],[0.0301003344481311,"#152F48"],[0.0334448160535127,"#152F48"],[0.0367892976588943,"#152F49"],[0.0401337792642001,"#153049"],[0.0434782608695817,"#16304A"],[0.0468227424748875,"#16304A"],[0.0501672240802691,"#16314B"],[0.0535117056856507,"#16314B"],[0.0568561872909565,"#16324C"],[0.0602006688963381,"#17324D"],[0.0635451505016438,"#17324D"],[0.0668896321070254,"#17334E"],[0.070234113712407,"#17334E"],[0.0735785953177128,"#17344F"],[0.0769230769230944,"#18344F"],[0.0802675585284002,"#183450"],[0.0836120401337818,"#183550"],[0.0869565217391634,"#183551"],[0.0903010033444692,"#183651"],[0.0936454849498508,"#193652"],[0.0969899665551566,"#193652"],[0.100334448160538,"#193753"],[0.10367892976592,"#193754"],[0.107023411371226,"#193854"],[0.110367892976607,"#1A3855"],[0.113712374581913,"#1A3955"],[0.117056856187295,"#1A3956"],[0.120401337792676,"#1A3956"],[0.123745819397982,"#1A3A57"],[0.127090301003363,"#1B3A57"],[0.130434782608669,"#1B3B58"],[0.133779264214051,"#1B3B59"],[0.137123745819432,"#1B3B59"],[0.140468227424738,"#1C3C5A"],[0.14381270903012,"#1C3C5A"],[0.147157190635426,"#1C3D5B"],[0.150501672240807,"#1C3D5B"],[0.153846153846189,"#1C3D5C"],[0.157190635451495,"#1D3E5C"],[0.160535117056876,"#1D3E5D"],[0.163879598662182,"#1D3F5D"],[0.167224080267564,"#1D3F5E"],[0.170568561872945,"#1D3F5F"],[0.173913043478251,"#1E405F"],[0.177257525083633,"#1E4060"],[0.180602006688938,"#1E4160"],[0.18394648829432,"#1E4161"],[0.187290969899702,"#1E4261"],[0.190635451505007,"#1F4262"],[0.193979933110389,"#1F4263"],[0.197324414715695,"#1F4363"],[0.200668896321076,"#1F4364"],[0.204013377926458,"#1F4464"],[0.207357859531764,"#204465"],[0.210702341137145,"#204465"],[0.214046822742451,"#204566"],[0.217391304347833,"#204566"],[0.220735785953214,"#214667"],[0.22408026755852,"#214668"],[0.227424749163902,"#214768"],[0.230769230769207,"#214769"],[0.234113712374589,"#214769"],[0.237458193979971,"#22486A"],[0.240802675585276,"#22486A"],[0.244147157190658,"#22496B"],[0.247491638795964,"#22496C"],[0.250836120401345,"#224A6C"],[0.254180602006651,"#234A6D"],[0.257525083612033,"#234A6D"],[0.260869565217414,"#234B6E"],[0.26421404682272,"#234B6E"],[0.267558528428102,"#244C6F"],[0.270903010033408,"#244C70"],[0.274247491638789,"#244C70"],[0.277591973244171,"#244D71"],[0.280936454849477,"#244D71"],[0.284280936454858,"#254E72"],[0.287625418060164,"#254E72"],[0.290969899665545,"#254F73"],[0.294314381270927,"#254F74"],[0.297658862876233,"#254F74"],[0.301003344481614,"#265075"],[0.30434782608692,"#265075"],[0.307692307692302,"#265176"],[0.311036789297683,"#265176"],[0.314381270902989,"#275277"],[0.317725752508371,"#275278"],[0.321070234113677,"#275278"],[0.324414715719058,"#275379"],[0.32775919732444,"#275379"],[0.331103678929746,"#28547A"],[0.334448160535127,"#28547B"],[0.337792642140433,"#28557B"],[0.341137123745815,"#28557C"],[0.344481605351196,"#28567C"],[0.347826086956502,"#29567D"],[0.351170568561884,"#29567D"],[0.354515050167189,"#29577E"],[0.357859531772571,"#29577F"],[0.361204013377953,"#2A587F"],[0.364548494983258,"#2A5880"],[0.36789297658864,"#2A5980"],[0.371237458193946,"#2A5981"],[0.374581939799327,"#2A5982"],[0.377926421404709,"#2B5A82"],[0.381270903010015,"#2B5A83"],[0.384615384615396,"#2B5B83"],[0.387959866220702,"#2B5B84"],[0.391304347826084,"#2C5C85"],[0.394648829431465,"#2C5C85"],[0.397993311036771,"#2C5D86"],[0.401337792642153,"#2C5D86"],[0.404682274247458,"#2C5D87"],[0.40802675585284,"#2D5E87"],[0.411371237458222,"#2D5E88"],[0.414715719063527,"#2D5F89"],[0.418060200668909,"#2D5F89"],[0.421404682274215,"#2E608A"],[0.424749163879596,"#2E608A"],[0.428093645484978,"#2E618B"],[0.431438127090284,"#2E618C"],[0.434782608695665,"#2E618C"],[0.438127090300971,"#2F628D"],[0.441471571906353,"#2F628D"],[0.444816053511734,"#2F638E"],[0.44816053511704,"#2F638F"],[0.451505016722422,"#30648F"],[0.454849498327728,"#306490"],[0.458193979933109,"#306590"],[0.461538461538491,"#306591"],[0.464882943143796,"#306592"],[0.468227424749178,"#316692"],[0.471571906354484,"#316693"],[0.474916387959865,"#316793"],[0.478260869565247,"#316794"],[0.481605351170553,"#326895"],[0.484949832775934,"#326895"],[0.48829431438124,"#326996"],[0.491638795986622,"#326996"],[0.494983277592003,"#326997"],[0.498327759197309,"#336A98"],[0.501672240802691,"#336A98"],[0.505016722407997,"#336B99"],[0.508361204013378,"#336B99"],[0.51170568561876,"#346C9A"],[0.515050167224066,"#346C9B"],[0.518394648829447,"#346D9B"],[0.521739130434753,"#346D9C"],[0.525083612040135,"#346E9D"],[0.528428093645516,"#356E9D"],[0.531772575250822,"#356E9E"],[0.535117056856203,"#356F9E"],[0.538461538461509,"#356F9F"],[0.541806020066891,"#3670A0"],[0.545150501672273,"#3670A0"],[0.548494983277578,"#3671A1"],[0.55183946488296,"#3671A1"],[0.555183946488266,"#3772A2"],[0.558528428093647,"#3772A3"],[0.561872909699029,"#3773A3"],[0.565217391304335,"#3773A4"],[0.568561872909716,"#3773A4"],[0.571906354515022,"#3874A5"],[0.575250836120404,"#3874A6"],[0.578595317725785,"#3875A6"],[0.581939799331091,"#3875A7"],[0.585284280936473,"#3976A8"],[0.588628762541778,"#3976A8"],[0.59197324414716,"#3977A9"],[0.595317725752542,"#3977A9"],[0.598662207357847,"#3978AA"],[0.602006688963229,"#3A78AB"],[0.605351170568535,"#3A79AB"],[0.608695652173916,"#3A79AC"],[0.612040133779298,"#3A79AC"],[0.615384615384604,"#3B7AAD"],[0.618729096989985,"#3B7AAE"],[0.622073578595291,"#3B7BAE"],[0.625418060200673,"#3B7BAF"],[0.628762541806054,"#3C7CB0"],[0.63210702341136,"#3C7CB0"],[0.635451505016742,"#3C7DB1"],[0.638795986622048,"#3C7DB1"],[0.642140468227429,"#3C7EB2"],[0.645484949832811,"#3D7EB3"],[0.648829431438116,"#3D7FB3"],[0.652173913043498,"#3D7FB4"],[0.655518394648804,"#3D7FB5"],[0.658862876254185,"#3E80B5"],[0.662207357859567,"#3E80B6"],[0.665551839464873,"#3E81B6"],[0.668896321070254,"#3E81B7"],[0.67224080267556,"#3F82B8"],[0.675585284280942,"#3F82B8"],[0.678929765886323,"#3F83B9"],[0.682274247491629,"#3F83BA"],[0.685618729097011,"#4084BA"],[0.688963210702317,"#4084BB"],[0.692307692307698,"#4085BB"],[0.69565217391308,"#4085BC"],[0.698996655518386,"#4086BD"],[0.702341137123767,"#4186BD"],[0.705685618729073,"#4186BE"],[0.709030100334454,"#4187BF"],[0.712374581939836,"#4187BF"],[0.715719063545142,"#4288C0"],[0.719063545150524,"#4288C1"],[0.722408026755829,"#4289C1"],[0.725752508361211,"#4289C2"],[0.729096989966592,"#438AC2"],[0.732441471571898,"#438AC3"],[0.73578595317728,"#438BC4"],[0.739130434782586,"#438BC4"],[0.742474916387967,"#438CC5"],[0.745819397993349,"#448CC6"],[0.749163879598655,"#448DC6"],[0.752508361204036,"#448DC7"],[0.755852842809342,"#448EC8"],[0.759197324414724,"#458EC8"],[0.762541806020029,"#458FC9"],[0.765886287625411,"#458FC9"],[0.769230769230793,"#458FCA"],[0.772575250836098,"#4690CB"],[0.77591973244148,"#4690CB"],[0.779264214046786,"#4691CC"],[0.782608695652167,"#4691CD"],[0.785953177257549,"#4792CD"],[0.789297658862855,"#4792CE"],[0.792642140468236,"#4793CF"],[0.795986622073542,"#4793CF"],[0.799331103678924,"#4894D0"],[0.802675585284305,"#4894D0"],[0.806020066889611,"#4895D1"],[0.809364548494993,"#4895D2"],[0.812709030100298,"#4896D2"],[0.81605351170568,"#4996D3"],[0.819397993311062,"#4997D4"],[0.822742474916367,"#4997D4"],[0.826086956521749,"#4998D5"],[0.829431438127055,"#4A98D6"],[0.832775919732436,"#4A99D6"],[0.836120401337818,"#4A99D7"],[0.839464882943124,"#4A9AD8"],[0.842809364548505,"#4B9AD8"],[0.846153846153811,"#4B9BD9"],[0.849498327759193,"#4B9BDA"],[0.852842809364574,"#4B9BDA"],[0.85618729096988,"#4C9CDB"],[0.859531772575262,"#4C9CDB"],[0.862876254180568,"#4C9DDC"],[0.866220735785949,"#4C9DDD"],[0.869565217391331,"#4D9EDD"],[0.872909698996637,"#4D9EDE"],[0.876254180602018,"#4D9FDF"],[0.879598662207324,"#4D9FDF"],[0.882943143812705,"#4DA0E0"],[0.886287625418087,"#4EA0E1"],[0.889632107023393,"#4EA1E1"],[0.892976588628774,"#4EA1E2"],[0.89632107023408,"#4EA2E3"],[0.899665551839462,"#4FA2E3"],[0.903010033444843,"#4FA3E4"],[0.906354515050149,"#4FA3E5"],[0.909698996655531,"#4FA4E5"],[0.913043478260837,"#50A4E6"],[0.916387959866218,"#50A5E7"],[0.9197324414716,"#50A5E7"],[0.923076923076906,"#50A6E8"],[0.926421404682287,"#51A6E8"],[0.929765886287593,"#51A7E9"],[0.933110367892975,"#51A7EA"],[0.936454849498356,"#51A8EA"],[0.939799331103662,"#52A8EB"],[0.943143812709044,"#52A9EC"],[0.946488294314349,"#52A9EC"],[0.949832775919731,"#52AAED"],[0.953177257525113,"#53AAEE"],[0.956521739130418,"#53ABEE"],[0.9598662207358,"#53ABEF"],[0.963210702341106,"#53ACF0"],[0.966555183946487,"#54ACF0"],[0.969899665551869,"#54ADF1"],[0.973244147157175,"#54ADF2"],[0.976588628762556,"#54AEF2"],[0.979933110367862,"#55AEF3"],[0.983277591973244,"#55AFF4"],[0.986622073578625,"#55AFF4"],[0.989966555183931,"#55B0F5"],[0.993311036789313,"#56B0F6"],[0.996655518394618,"#56B1F6"],[1,"#56B1F7"]],"colorbar":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"thickness":23.04,"title":"date","titlefont":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"tickmode":"array","ticktext":["Jul 15","Aug 01","Aug 15"],"tickvals":[0.145833333333333,0.5,0.791666666666667],"tickfont":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"ticklen":2,"len":0.5}},"xaxis":"x","yaxis":"y","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":40.1826484018265,"l":48.9497716894977},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"~Date of greatest cucumber yield by weight in grams~","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[18448.105,18501.895],"tickmode":"array","ticktext":["07/06/20","07/13/20","07/20/20","07/27/20","08/03/20","08/10/20","08/17/20","08/24/20"],"tickvals":[18449,18456,18463,18470,18477,18484,18491,18498],"categoryorder":"array","categoryarray":["07/06/20","07/13/20","07/20/20","07/27/20","08/03/20","08/10/20","08/17/20","08/24/20"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"DATE","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-156.05,3277.05],"tickmode":"array","ticktext":["0","1000","2000","3000"],"tickvals":[0,1000,2000,3000],"categoryorder":"array","categoryarray":["0","1000","2000","3000"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"WEIGHT","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"fd3eeee8989":{"x":{},"y":{},"fill":{},"type":"bar"}},"cur_data":"fd3eeee8989","visdat":{"fd3eeee8989":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```




```r
improved_cucumber_weight <- garden_harvest %>% 
  select(vegetable, date, weight, variety) %>% 
  filter(vegetable %in% c("cucumbers")) %>% 
  group_by(vegetable, variety, date) %>% 
  summarize(weight_in_lbs = sum(weight*0.00220462)) %>% 
  arrange(desc(weight_in_lbs)) %>% 
  
  ggplot(aes(y = weight_in_lbs, x = date, fill = (weight_in_lbs)))+
  geom_col() +
  
  scale_fill_viridis_c(direction = -1)+
  
  scale_x_date(date_breaks = "1 week", date_labels = "%D") +
  
  labs(title = "Which week yielded the greatest pickling cucumber harvest in pounds?",
       x = "", 
       y = "Pounds",
       fill = "",
       caption = "By Cat Terres. Data sourced from garden_harvest, provided by Lisa Lendway") +
  theme_grey()

ggplotly(improved_cucumber_weight)
```

```{=html}
<div id="htmlwidget-f0fe838c6c7821a0f65f" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-f0fe838c6c7821a0f65f">{"x":{"data":[{"orientation":"v","width":0.900000000001455,"base":0,"x":[18456],"y":[0.10361714],"text":"date: 2020-07-13<br />weight_in_lbs: 0.1036171<br />(weight_in_lbs): 0.1036171","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(253,231,37,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18494],"y":[0.1543234],"text":"date: 2020-08-20<br />weight_in_lbs: 0.1543234<br />(weight_in_lbs): 0.1543234","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(249,230,40,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18471],"y":[0.16755112],"text":"date: 2020-07-28<br />weight_in_lbs: 0.1675511<br />(weight_in_lbs): 0.1675511","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(247,230,40,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18452],"y":[0.17196036],"text":"date: 2020-07-09<br />weight_in_lbs: 0.1719604<br />(weight_in_lbs): 0.1719604","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(247,230,41,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18480],"y":[0.27998674],"text":"date: 2020-08-06<br />weight_in_lbs: 0.2799867<br />(weight_in_lbs): 0.2799867","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(238,229,46,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18455],"y":[0.2866006],"text":"date: 2020-07-12<br />weight_in_lbs: 0.2866006<br />(weight_in_lbs): 0.2866006","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(237,228,46,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18457],"y":[0.33510224],"text":"date: 2020-07-14<br />weight_in_lbs: 0.3351022<br />(weight_in_lbs): 0.3351022","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(233,228,48,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18474],"y":[0.38360388],"text":"date: 2020-07-31<br />weight_in_lbs: 0.3836039<br />(weight_in_lbs): 0.3836039","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(228,227,50,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[0.900000000001455,0.900000000001455],"base":[0,0],"x":[18463,18499],"y":[0.39462698,0.39462698],"text":["date: 2020-07-20<br />weight_in_lbs: 0.3946270<br />(weight_in_lbs): 0.3946270","date: 2020-08-25<br />weight_in_lbs: 0.3946270<br />(weight_in_lbs): 0.3946270"],"type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(227,227,50,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18451],"y":[0.39903622],"text":"date: 2020-07-08<br />weight_in_lbs: 0.3990362<br />(weight_in_lbs): 0.3990362","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(227,227,51,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18461],"y":[0.64815828],"text":"date: 2020-07-18<br />weight_in_lbs: 0.6481583<br />(weight_in_lbs): 0.6481583","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(205,223,60,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18460],"y":[0.76500314],"text":"date: 2020-07-17<br />weight_in_lbs: 0.7650031<br />(weight_in_lbs): 0.7650031","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(194,221,63,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18489],"y":[0.77382162],"text":"date: 2020-08-15<br />weight_in_lbs: 0.7738216<br />(weight_in_lbs): 0.7738216","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(193,221,63,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18472],"y":[1.13317468],"text":"date: 2020-07-29<br />weight_in_lbs: 1.1331747<br />(weight_in_lbs): 1.1331747","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(158,215,73,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18467],"y":[1.1574255],"text":"date: 2020-07-24<br />weight_in_lbs: 1.1574255<br />(weight_in_lbs): 1.1574255","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(155,214,74,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18462],"y":[1.17065322],"text":"date: 2020-07-19<br />weight_in_lbs: 1.1706532<br />(weight_in_lbs): 1.1706532","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(154,214,74,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18487],"y":[1.32056738],"text":"date: 2020-08-13<br />weight_in_lbs: 1.3205674<br />(weight_in_lbs): 1.3205674","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(138,212,78,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18473],"y":[1.38009212],"text":"date: 2020-07-30<br />weight_in_lbs: 1.3800921<br />(weight_in_lbs): 1.3800921","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(131,210,79,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18465],"y":[1.4440261],"text":"date: 2020-07-22<br />weight_in_lbs: 1.4440261<br />(weight_in_lbs): 1.4440261","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(124,209,81,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18497],"y":[1.64685114],"text":"date: 2020-08-23<br />weight_in_lbs: 1.6468511<br />(weight_in_lbs): 1.6468511","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(114,203,90,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18470],"y":[1.7306267],"text":"date: 2020-07-27<br />weight_in_lbs: 1.7306267<br />(weight_in_lbs): 1.7306267","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(110,201,93,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18468],"y":[1.98636262],"text":"date: 2020-07-25<br />weight_in_lbs: 1.9863626<br />(weight_in_lbs): 1.9863626","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(98,193,103,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18495],"y":[2.19800614],"text":"date: 2020-08-21<br />weight_in_lbs: 2.1980061<br />(weight_in_lbs): 2.1980061","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(86,186,111,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18485],"y":[2.26855398],"text":"date: 2020-08-11<br />weight_in_lbs: 2.2685540<br />(weight_in_lbs): 2.2685540","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(82,184,114,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18458],"y":[2.33028334],"text":"date: 2020-07-15<br />weight_in_lbs: 2.3302833<br />(weight_in_lbs): 2.3302833","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(78,182,116,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18475],"y":[2.4912206],"text":"date: 2020-08-01<br />weight_in_lbs: 2.4912206<br />(weight_in_lbs): 2.4912206","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(67,178,121,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18477],"y":[2.5463361],"text":"date: 2020-08-03<br />weight_in_lbs: 2.5463361<br />(weight_in_lbs): 2.5463361","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(63,176,123,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18481],"y":[2.92553074],"text":"date: 2020-08-07<br />weight_in_lbs: 2.9255307<br />(weight_in_lbs): 2.9255307","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(36,164,133,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18482],"y":[3.74124014],"text":"date: 2020-08-08<br />weight_in_lbs: 3.7412401<br />(weight_in_lbs): 3.7412401","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(44,135,139,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":0.900000000001455,"base":0,"x":[18492],"y":[6.88061902],"text":"date: 2020-08-18<br />weight_in_lbs: 6.8806190<br />(weight_in_lbs): 6.8806190","type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(68,1,84,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[18449],"y":[0],"name":"99_2493a81de04b122bb84657343a4b333b","type":"scatter","mode":"markers","opacity":0,"hoverinfo":"skip","showlegend":false,"marker":{"color":[0,1],"colorscale":[[0,"#FDE725"],[0.00334448160535117,"#FBE726"],[0.00668896321070234,"#F9E627"],[0.0100334448160535,"#F7E629"],[0.0133779264214047,"#F5E62A"],[0.0167224080267559,"#F3E52B"],[0.020066889632107,"#F1E52C"],[0.0234113712374582,"#EFE52D"],[0.0267558528428094,"#EDE42E"],[0.0301003344481605,"#EBE42F"],[0.0334448160535117,"#E9E430"],[0.0367892976588629,"#E7E331"],[0.040133779264214,"#E5E332"],[0.0434782608695652,"#E3E333"],[0.0468227424749164,"#E1E233"],[0.0501672240802676,"#DFE234"],[0.0535117056856187,"#DDE235"],[0.0568561872909699,"#DBE136"],[0.0602006688963211,"#D9E137"],[0.0635451505016722,"#D7E138"],[0.0668896321070234,"#D5E038"],[0.0702341137123746,"#D3E039"],[0.0735785953177258,"#D1E03A"],[0.0769230769230769,"#CFDF3B"],[0.0802675585284281,"#CDDF3B"],[0.0836120401337793,"#CBDF3C"],[0.0869565217391304,"#C8DE3D"],[0.0903010033444816,"#C6DE3E"],[0.0936454849498328,"#C4DE3E"],[0.096989966555184,"#C2DD3F"],[0.100334448160535,"#C0DD40"],[0.103678929765886,"#BEDC40"],[0.107023411371237,"#BCDC41"],[0.110367892976589,"#BADC42"],[0.11371237458194,"#B7DB42"],[0.117056856187291,"#B5DB43"],[0.120401337792642,"#B3DB44"],[0.123745819397993,"#B1DA44"],[0.127090301003344,"#AFDA45"],[0.130434782608696,"#ACD946"],[0.133779264214047,"#AAD946"],[0.137123745819398,"#A8D947"],[0.140468227424749,"#A6D847"],[0.1438127090301,"#A3D848"],[0.147157190635452,"#A1D748"],[0.150501672240803,"#9FD749"],[0.153846153846154,"#9DD74A"],[0.157190635451505,"#9AD64A"],[0.160535117056856,"#98D64B"],[0.163879598662207,"#95D54B"],[0.167224080267559,"#93D54C"],[0.17056856187291,"#91D54C"],[0.173913043478261,"#8ED44D"],[0.177257525083612,"#8CD44D"],[0.180602006688963,"#89D34E"],[0.183946488294314,"#87D34F"],[0.187290969899666,"#84D34F"],[0.190635451505017,"#81D250"],[0.193979933110368,"#7FD250"],[0.197324414715719,"#7CD151"],[0.20066889632107,"#7AD151"],[0.204013377926421,"#79D052"],[0.207357859531773,"#78CF53"],[0.210702341137124,"#77CF54"],[0.214046822742475,"#76CE55"],[0.217391304347826,"#75CD56"],[0.220735785953177,"#74CD57"],[0.224080267558528,"#73CC58"],[0.22742474916388,"#72CB59"],[0.230769230769231,"#71CB5A"],[0.234113712374582,"#70CA5B"],[0.237458193979933,"#6FC95C"],[0.240802675585284,"#6EC85D"],[0.244147157190635,"#6DC85E"],[0.247491638795987,"#6CC75F"],[0.250836120401338,"#6BC660"],[0.254180602006689,"#6AC661"],[0.25752508361204,"#69C562"],[0.260869565217391,"#67C463"],[0.264214046822742,"#66C464"],[0.267558528428094,"#65C365"],[0.270903010033445,"#64C266"],[0.274247491638796,"#63C166"],[0.277591973244147,"#62C167"],[0.280936454849498,"#61C068"],[0.28428093645485,"#5FBF69"],[0.287625418060201,"#5EBF6A"],[0.290969899665552,"#5DBE6B"],[0.294314381270903,"#5CBD6C"],[0.297658862876254,"#5BBD6C"],[0.301003344481605,"#59BC6D"],[0.304347826086956,"#58BB6E"],[0.307692307692308,"#57BB6F"],[0.311036789297659,"#55BA70"],[0.31438127090301,"#54B971"],[0.317725752508361,"#53B971"],[0.321070234113712,"#51B872"],[0.324414715719064,"#50B773"],[0.327759197324415,"#4EB674"],[0.331103678929766,"#4DB675"],[0.334448160535117,"#4BB575"],[0.337792642140468,"#4AB476"],[0.341137123745819,"#48B477"],[0.344481605351171,"#47B378"],[0.347826086956522,"#45B278"],[0.351170568561873,"#43B279"],[0.354515050167224,"#42B17A"],[0.357859531772575,"#40B07B"],[0.361204013377926,"#3EB07B"],[0.364548494983278,"#3CAF7C"],[0.367892976588629,"#3AAE7D"],[0.37123745819398,"#38AE7E"],[0.374581939799331,"#36AD7E"],[0.377926421404682,"#34AC7F"],[0.381270903010033,"#32AC80"],[0.384615384615385,"#2FAB81"],[0.387959866220736,"#2DAA81"],[0.391304347826087,"#2AAA82"],[0.394648829431438,"#27A983"],[0.397993311036789,"#24A884"],[0.40133779264214,"#22A884"],[0.404682274247492,"#23A784"],[0.408026755852843,"#23A684"],[0.411371237458194,"#24A585"],[0.414715719063545,"#24A485"],[0.418060200668896,"#25A485"],[0.421404682274247,"#25A385"],[0.424749163879599,"#26A285"],[0.42809364548495,"#26A186"],[0.431438127090301,"#26A086"],[0.434782608695652,"#27A086"],[0.438127090301003,"#279F86"],[0.441471571906354,"#279E86"],[0.444816053511706,"#289D87"],[0.448160535117057,"#289C87"],[0.451505016722408,"#289B87"],[0.454849498327759,"#299B87"],[0.45819397993311,"#299A87"],[0.461538461538462,"#299987"],[0.464882943143813,"#299888"],[0.468227424749164,"#2A9788"],[0.471571906354515,"#2A9788"],[0.474916387959866,"#2A9688"],[0.478260869565217,"#2A9588"],[0.481605351170569,"#2A9489"],[0.48494983277592,"#2A9389"],[0.488294314381271,"#2B9389"],[0.491638795986622,"#2B9289"],[0.494983277591973,"#2B9189"],[0.498327759197324,"#2B9089"],[0.501672240802676,"#2B8F8A"],[0.505016722408027,"#2B8F8A"],[0.508361204013378,"#2B8E8A"],[0.511705685618729,"#2B8D8A"],[0.51505016722408,"#2B8C8A"],[0.518394648829431,"#2B8B8A"],[0.521739130434783,"#2C8B8B"],[0.525083612040134,"#2C8A8B"],[0.528428093645485,"#2C898B"],[0.531772575250836,"#2C888B"],[0.535117056856187,"#2C878B"],[0.538461538461538,"#2C878B"],[0.54180602006689,"#2C868B"],[0.545150501672241,"#2C858C"],[0.548494983277592,"#2C848C"],[0.551839464882943,"#2C838C"],[0.555183946488294,"#2B838C"],[0.558528428093645,"#2B828C"],[0.561872909698997,"#2B818C"],[0.565217391304348,"#2B808D"],[0.568561872909699,"#2B7F8D"],[0.57190635451505,"#2B7F8D"],[0.575250836120401,"#2B7E8D"],[0.578595317725753,"#2B7D8D"],[0.581939799331104,"#2B7C8D"],[0.585284280936455,"#2B7B8D"],[0.588628762541806,"#2B7B8E"],[0.591973244147157,"#2A7A8E"],[0.595317725752508,"#2A798E"],[0.59866220735786,"#2A788E"],[0.602006688963211,"#2B778E"],[0.605351170568562,"#2B778E"],[0.608695652173913,"#2C768E"],[0.612040133779264,"#2D758E"],[0.615384615384615,"#2E748E"],[0.618729096989966,"#2F738D"],[0.622073578595318,"#2F728D"],[0.625418060200669,"#30718D"],[0.62876254180602,"#31718D"],[0.632107023411371,"#31708D"],[0.635451505016722,"#326F8D"],[0.638795986622074,"#326E8D"],[0.642140468227425,"#336D8D"],[0.645484949832776,"#346C8D"],[0.648829431438127,"#346B8C"],[0.652173913043478,"#356B8C"],[0.655518394648829,"#356A8C"],[0.658862876254181,"#36698C"],[0.662207357859532,"#36688C"],[0.665551839464883,"#37678C"],[0.668896321070234,"#37668C"],[0.672240802675585,"#38658C"],[0.675585284280936,"#38658C"],[0.678929765886288,"#38648B"],[0.682274247491639,"#39638B"],[0.68561872909699,"#39628B"],[0.688963210702341,"#3A618B"],[0.692307692307692,"#3A608B"],[0.695652173913044,"#3A5F8B"],[0.698996655518395,"#3B5F8B"],[0.702341137123746,"#3B5E8B"],[0.705685618729097,"#3B5D8A"],[0.709030100334448,"#3C5C8A"],[0.712374581939799,"#3C5B8A"],[0.715719063545151,"#3C5A8A"],[0.719063545150502,"#3D598A"],[0.722408026755853,"#3D598A"],[0.725752508361204,"#3D588A"],[0.729096989966555,"#3D578A"],[0.732441471571906,"#3E568A"],[0.735785953177257,"#3E5589"],[0.739130434782609,"#3E5489"],[0.74247491638796,"#3E5389"],[0.745819397993311,"#3F5289"],[0.749163879598662,"#3F5289"],[0.752508361204013,"#3F5189"],[0.755852842809364,"#3F5089"],[0.759197324414716,"#3F4F89"],[0.762541806020067,"#404E88"],[0.765886287625418,"#404D88"],[0.769230769230769,"#404C88"],[0.77257525083612,"#404B88"],[0.775919732441472,"#404A88"],[0.779264214046823,"#404A88"],[0.782608695652174,"#404988"],[0.785953177257525,"#414888"],[0.789297658862876,"#414787"],[0.792642140468227,"#414687"],[0.795986622073579,"#414587"],[0.79933110367893,"#414487"],[0.802675585284281,"#414386"],[0.806020066889632,"#424285"],[0.809364548494983,"#424185"],[0.812709030100334,"#424184"],[0.816053511705686,"#424083"],[0.819397993311037,"#433F82"],[0.822742474916388,"#433E81"],[0.826086956521739,"#433D80"],[0.82943143812709,"#433C7F"],[0.832775919732442,"#433B7E"],[0.836120401337793,"#443A7D"],[0.839464882943144,"#44397D"],[0.842809364548495,"#44387C"],[0.846153846153846,"#44377B"],[0.849498327759197,"#44367A"],[0.852842809364548,"#443679"],[0.8561872909699,"#443578"],[0.859531772575251,"#453477"],[0.862876254180602,"#453377"],[0.866220735785953,"#453276"],[0.869565217391304,"#453175"],[0.872909698996655,"#453074"],[0.876254180602007,"#452F73"],[0.879598662207358,"#452E72"],[0.882943143812709,"#452D71"],[0.88628762541806,"#452C70"],[0.889632107023411,"#452B70"],[0.892976588628763,"#462A6F"],[0.896321070234114,"#46296E"],[0.899665551839465,"#46286D"],[0.903010033444816,"#46276C"],[0.906354515050167,"#46266B"],[0.909698996655518,"#46256B"],[0.91304347826087,"#46246A"],[0.916387959866221,"#462369"],[0.919732441471572,"#462268"],[0.923076923076923,"#462167"],[0.926421404682274,"#462066"],[0.929765886287625,"#461F65"],[0.933110367892977,"#461E65"],[0.936454849498328,"#461D64"],[0.939799331103679,"#461B63"],[0.94314381270903,"#461A62"],[0.946488294314381,"#451961"],[0.949832775919732,"#451860"],[0.953177257525084,"#451760"],[0.956521739130435,"#45155F"],[0.959866220735786,"#45145E"],[0.963210702341137,"#45135D"],[0.966555183946488,"#45115C"],[0.969899665551839,"#45105B"],[0.973244147157191,"#450E5B"],[0.976588628762542,"#450D5A"],[0.979933110367893,"#450B59"],[0.983277591973244,"#450958"],[0.986622073578595,"#450857"],[0.989966555183946,"#440656"],[0.993311036789298,"#440456"],[0.996655518394649,"#440355"],[1,"#440154"]],"colorbar":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.88976377952756,"thickness":23.04,"title":"","titlefont":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"tickmode":"array","ticktext":["2","4","6"],"tickvals":[0.279826226047911,0.574941977144619,0.870057728241327],"tickfont":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"ticklen":2,"len":0.5}},"xaxis":"x","yaxis":"y","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":31.4155251141553},"plot_bgcolor":"rgba(235,235,235,1)","paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Which week yielded the greatest pickling cucumber harvest in pounds?","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[18448.105,18501.895],"tickmode":"array","ticktext":["07/06/20","07/13/20","07/20/20","07/27/20","08/03/20","08/10/20","08/17/20","08/24/20"],"tickvals":[18449,18456,18463,18470,18477,18484,18491,18498],"categoryorder":"array","categoryarray":["07/06/20","07/13/20","07/20/20","07/27/20","08/03/20","08/10/20","08/17/20","08/24/20"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-0.344030951,7.224649971],"tickmode":"array","ticktext":["0","2","4","6"],"tickvals":[0,2,4,6],"categoryorder":"array","categoryarray":["0","2","4","6"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"Pounds","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.88976377952756,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"fd3e704b3185":{"x":{},"y":{},"fill":{},"type":"bar"}},"cur_data":"fd3e704b3185","visdat":{"fd3e704b3185":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

  
  2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).
  
<img src="05_exercises_new_files/figure-html/unnamed-chunk-3-1.gif" title="This animation shows the number of late arrivals at each of the ten selected stations. The dot colors correspond to each station and reveal one after the other from least to greatest." alt="This animation shows the number of late arrivals at each of the ten selected stations. The dot colors correspond to each station and reveal one after the other from least to greatest."  />



![](latearrivals.gif)<!-- -->
## Garden data

  3. In this exercise, you will create a stacked area plot that reveals itself over time (see the `geom_area()` examples [here](https://ggplot2.tidyverse.org/reference/position_stack.html)). You will look at cumulative harvest of tomato varieties over time. I have filtered the data to the tomatoes and find the *daily* harvest in pounds for each variety. The `complete()` function creates a row for all unique `date`/`variety` combinations. If a variety is not harvested on one of the harvest dates in the dataset, it is filled with a value of 0. 
  You should do the following:
  * For each variety, find the cumulative harvest in pounds.  
  * Use the data you just made to create a static cumulative harvest area plot, with the areas filled with different colors for each variety and arranged (HINT: `fct_reorder()`) from most to least harvested weights (most on the bottom).  
  * Add animation to reveal the plot over date. Instead of having a legend, place the variety names directly on the graph (refer back to the tutorial for how to do this).


```r
garden_harvest %>% 
  filter(vegetable == "tomatoes") %>% 
  group_by(date, variety) %>% 
  summarize(daily_harvest_lb = sum(weight)*0.00220462) %>% 
  ungroup() %>% 
  mutate(cum_harvest = cumsum(daily_harvest_lb)) %>% 
  complete(variety, 
           date, 
           fill = list(daily_harvest_lb = 0)) %>% 
  group_by(variety) %>% 
  mutate(cum_harvest_lb = sum(daily_harvest_lb)) %>% 
  
  ggplot(aes(x = date,
             y = daily_harvest_lb,
             fill = fct_reorder(variety, cum_harvest_lb)))+
  geom_area()+
  geom_text(aes(label=variety))+
  labs(title = "Cumulative Harvest of Tomato Varieties Over Time",
       subtitle = "Date: {frame_along}",
       fill = "Variety",
       caption = "Graph and animation by Cat Terres; data from garden_harvest")+
  transition_reveal(date)
```

<img src="05_exercises_new_files/figure-html/unnamed-chunk-6-1.gif" title="This graph overlays the cumulative harvest of each tomato variety over one another as an area graph. Each variety has a color, and the animation fills in from left to right with the names of each variety following its respective plot." alt="This graph overlays the cumulative harvest of each tomato variety over one another as an area graph. Each variety has a color, and the animation fills in from left to right with the names of each variety following its respective plot."  />


## Maps, animation, and movement!

  4. Map Lisa's `mallorca_bike_day7` bike ride using animation! 
  Requirements:
  * Plot on a map using `ggmap`.  #
  * Show "current" location with a red point. 
  * Show path up until the current point.#   
  * Color the path according to elevation.  #
  * Show the time in the subtitle.  #
  * CHALLENGE: use the `ggimage` package and `geom_image` to add a bike image instead of a red point. You can use [this](https://raw.githubusercontent.com/llendway/animation_and_interactivity/master/bike.png) image. See [here](https://goodekat.github.io/presentations/2019-isugg-gganimate-spooky/slides.html#35) for an example. 
  * Add something of your own! And comment on if you prefer this to the static map and why or why not.
  


```r
mallorca_map <- get_stamenmap(
    bbox = c(left = 2.2809, bottom = 39.4418, right = 3.0191, top = 39.7751), 
    maptype = "terrain",
    zoom = 10 
)

ggmap(mallorca_map)
```

![](05_exercises_new_files/figure-html/unnamed-chunk-7-1.png)<!-- -->


```r
mallorca_map <- get_stamenmap(
    bbox = c(left = 2.2809, bottom = 39.4418, right = 3.0191, top = 39.7751), 
    maptype = "terrain",
    zoom = 9
)
```


```r
ggmap(mallorca_map) +
  geom_point(data = mallorca_bike_day7,
             aes(x = lon, y = lat, size = speed),
                 color = "red")+
  geom_path(data = mallorca_bike_day7 , 
             aes(x = lon, y = lat, color = ele),
             size = .5) +
  labs(title = "Lisa's Bike Ride",
       subtitle = "Timestamp: {frame_along}",
       x = "", 
       y = "",
       caption = "Animation by Cat Terres; data sourced from mallorca_bike_day7 by Lisa Lendway.")+
  scale_color_viridis_c(option = "magma") +
  theme_map() +
  theme(legend.background = element_blank())+
  transition_reveal(time)
```

<img src="05_exercises_new_files/figure-html/unnamed-chunk-9-1.gif" title="Lisa's Bike ride! Here is a map of the island of Mallorca, zoomed in to show the circuitous bike route taken. It is colored by elevation, with the lighter colors indicating higher points of elevation, and a dot that follows the current location, changing in size based on the speed at that given time." alt="Lisa's Bike ride! Here is a map of the island of Mallorca, zoomed in to show the circuitous bike route taken. It is colored by elevation, with the lighter colors indicating higher points of elevation, and a dot that follows the current location, changing in size based on the speed at that given time."  />


```r
anim_save("bike_ride.gif")
```


```r
knitr::include_graphics("bike_ride.gif")
```

![](bike_ride.gif)<!-- -->



##c(left = 2.1190, bottom = 39.2057, right = 3.5, top = 40)
  
  5. In this exercise, you get to meet Lisa's sister, Heather! She is a proud Mac grad, currently works as a Data Scientist where she uses R everyday, and for a few years (while still holding a full-time job) she was a pro triathlete. You are going to map one of her races. The data from each discipline of the Ironman 70.3 Pan Am championships, Panama is in a separate file - `panama_swim`, `panama_bike`, and `panama_run`. Create a similar map to the one you created with my cycling data. You will need to make some small changes: 1. combine the files putting them in swim, bike, run order (HINT: `bind_rows()`), 2. #####make the leading dot a different color depending on the event### (for an extra challenge, make it a different image using `geom_image()!), 3. CHALLENGE (optional): color by speed, which you will need to compute on your own from the data. You can read Heather's race report [here](https://heatherlendway.com/2016/02/10/ironman-70-3-pan-american-championships-panama-race-report/). She is also in the Macalester Athletics [Hall of Fame](https://athletics.macalester.edu/honors/hall-of-fame/heather-lendway/184) and still has records at the pool. 



```r
panama_map <-get_stamenmap(
 bbox = c(left = -79.6114, bottom = 8.9049, right = -79.4268, top = 9.0118), 
    maptype = "terrain",
    zoom = 12
)
ggmap(panama_map)
```

![](05_exercises_new_files/figure-html/unnamed-chunk-12-1.png)<!-- -->


```r
swim_bike_run <- bind_rows(panama_swim,panama_bike, panama_run)
```


```r
ggmap(panama_map) +
  geom_point(data = swim_bike_run,
             aes(x = lon, y = lat, color = event),
             size = 5)+
  geom_path(data = swim_bike_run, 
             aes(x = lon, y = lat),
             size = .5) +
  labs(title = "Heather's Triathlon",
       subtitle = "Timestamp: {frame_along}",
       color = "Event",
       caption= "Animation by Cat Terres; data from panama_swim, panama_bike, and panama_run")+
  theme_map() +
  theme(legend.background = element_blank())+
  transition_reveal(time)
```

<img src="05_exercises_new_files/figure-html/unnamed-chunk-14-1.gif" title="Yay Triathlon! This dataset is a combination of swimming, biking, and running data gathered from a triathlon route. Each discipline is indicated by its own colored dot that follows the path taken." alt="Yay Triathlon! This dataset is a combination of swimming, biking, and running data gathered from a triathlon route. Each discipline is indicated by its own colored dot that follows the path taken."  />
  

```r
anim_save("heather_tri.gif")
```


```r
knitr::include_graphics("heather_tri.gif")
```

![](heather_tri.gif)<!-- -->
## COVID-19 data

  6. In this exercise you will animate a map of the US, showing how cumulative COVID-19 cases per 10,000 residents has changed over time. This is similar to exercises 11 & 12 from the previous exercises, with the added animation! So, in the end, you should have something like the static map you made there, but animated over all the days. The code below gives the population estimates for each state and loads the `states_map` data. Here is a list of details you should include in the plot:
  
  * Put date in the subtitle.   
  * Because there are so many dates, you are going to only do the animation for the the 15th of each month. So, filter only to those dates - there are some lubridate functions that can help you do this.   
  * Use the `animate()` function to make the animation 200 frames instead of the default 100 and to pause for 10 frames on the end frame.   
  * Use `group = date` in `aes()`.   
  * Comment on what you see.  


```r
census_pop_est_2018 <- read_csv("https://www.dropbox.com/s/6txwv3b4ng7pepe/us_census_2018_state_pop_est.csv?dl=1") %>% 
  separate(state, into = c("dot","state"), extra = "merge") %>% 
  select(-dot) %>% 
  mutate(state = str_to_lower(state))

states_map <- map_data("state")
```


```r
newest_covid <- covid19 %>% 
  arrange(desc(date)) %>% 
  group_by(state) %>% 
  mutate(numberrow = 1:n()) %>% 
  mutate(state = str_to_lower(`state`))

covid_by_pop <- newest_covid %>% 
  left_join(census_pop_est_2018,
            by = c("state" = "state")) %>% 
  mutate(per_10000 = (cases/est_pop_2018)*10000)

us_covid_gif <- covid_by_pop %>% 
  filter(day(date) == 15)  %>% 
  ggplot() +
  geom_map(map = states_map,
           aes(map_id = state,
               fill = per_10000)) +
  labs(title = "Most Recent Cumulative Count of COVID-19 Cases by State Factoring in Population Density", 
       fill = "Cases per 10,000", 
       subtitle = "Date: {frame_along}",
       caption = "Animation and map by Cat Terres; data from covid19 and census_pop_est_2018") +
  expand_limits(x = states_map$long, y = states_map$lat) + 
  scale_fill_viridis_c(option = "rocket", direction = -1) +
  theme_map() + 
  theme(legend.background = element_blank())+
  transition_reveal(date)


animate(us_covid_gif, nframes = 200, end_pause = 10)
anim_save("us_covid_gif.gif")
```
![](us_covid_gif.gif)<!-- -->
## Your first `shiny` app (for next week!)

  7. This app will also use the COVID data. Make sure you load that data and all the libraries you need in the `app.R` file you create. You should create a new project for the app, separate from the homework project. Below, you will post a link to the app that you publish on shinyapps.io. You will create an app to compare states' daily number of COVID cases per 100,000 over time. The x-axis will be date. You will have an input box where the user can choose which states to compare (`selectInput()`), a slider where the user can choose the date range, and a submit button to click once the user has chosen all states they're interested in comparing. The graph should display a different line for each state, with labels either on the graph or in a legend. Color can be used if needed. 
  


  
Put the link to your app here: 
  
https://cterres.shinyapps.io/firstshiny/

## GitHub link

  8. Below, provide a link to your GitHub repo with this set of Weekly Exercises. 

https://github.com/cterres/Exercise5


**DID YOU REMEMBER TO UNCOMMENT THE OPTIONS AT THE TOP?**
