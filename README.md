# bbbiodiversity-challenge

As always, I would like to give a shoutout to TA Drew, who always provides his assistance with his speedruns.

In this challenge, I was able to successfuly create a dashboard for the belly button biodiversity of multiple samples using javascript and html. Here I will be explaining the functionality of the dashboard, the code behind the dashboard, and ways I would like to improve on the current design.

I. Dashboard Functionality

For each belly button sample (identified by their Test Subject ID Number) which are selectable via a dropdown menu near the upper left corner below the heading, there are four charts that are displayed based on data for that sample.

The first is a small table containing metadata about the sample under "Demographic Info. It contains information about the sample ID (as selected from the dropdown menu), details about the person who the sample was collected from (ethnicity, gender, age, location and belly button type), and how many times they washed their belly button in a week (wfreq). 

Directly to the right of the table is a horizontal bar chart ("Top 10 Bacterial Cultures Found") of the top 10 most identified bacterial cultures identified based on their operational tax unit (OTU in the chart). More identifications placed the identified OTUs closer to the top. Hovering your cursor over each bar will reveal the count of bacterial cultures identified with the OTU and the specific taxonomic information related to the OTU. Some are specific enough down to the genus level, while others do not list more information beyond the domain (Bacteria) with many in between their extent of specificity. Note that some samples may not list 10 identified cultures (Sample ID # 943 only has one), so the bar chart may display less than 10 identified cultures.

Directly to the right of the bar chart is a gauge of belly button washing frequency (measured in scrubs per week). This directly references the wfreq information of the sample from the table and illustrates the frequency of washing the belly button from the person whom the sample was collected from. The needle will point towards the line between two sections which intersect at a common number (ex. Sample ID #940 lists a wfreq of 2, so the gauge will point in between the sections of "1-2", "2-3"). You can scroll over elements of the gauge chart, however, they do not provide extra information that would be relevant to interpretation of the data (the gauge sections list their titles, the needle lists their angle relative to when the needle is pointed to the left, and scrolling over the bottom of the gauge reveals a white section that serves no function to illustrate data). In the case that no information is listed in "wfreq" (wfreq = null, different from the case of wfreq = 0), the needle will not display on the gauge.

At the bottom of the page, there is a bubble chart listing the frequency of the cultures identified within the sample. This is an extension of the bar chart in that it lists all of the bacterial cultures identified in the sample including those that were not the top 10 most frequently identified. On the x-axis is the OTU ID # of the sample identified in question, while on the y-axis is the count that they were identified. The center of each bubble is centered around each point based on the coordinates of (OTU ID #, count identified) while the bubbles are sized relative to their frequencies. Higher frequencies indicate bigger bubbles. Scrolling over these bubbles indicate their coordinates as mentioned earlier and their taxonomic information. In the case of overlapping bubbles, the bubble that has a smaller frequency (and thus smaller size) generally tends to have their information displayed at a higher priority than the bubble with a higher frequency (or a bigger size).


II. Explanation of the Data's Code

The index.html file contains the basic structure of the website the dashboard functions on. The only change made here was a reorganization of the order the javascript files would be printed in.

In the samples.json file, there is an array that contains information about the samples. "names" correlates to the sample ID #s, metadata was explained in the demographics table, and "samples" contains information about the otu's identified in each sample. Nothing was altered here.

In the static folder, there are two javascript (js) files. The main bulk of the website's code is found in app.js. It contains multiple functions to create all the individual elements you can see. I assigned quite a few variables to certain sections of the data found in the json file to keep the code in shorthand. 

The bar chart and bubble chart were created using the Plotly.newPlot function, using the data in the json file to create both the layouts and data accepted in the arguments for the newPlot function.
The metadata table was created with the PANEL function referencing the json file for each sample's metadata.
At the bottom included the Gauge function used in the other js file mentioned later.
Finally, the init function allowed for the site to utilize the functions created earlier to construct the charts onto the site. This also include functionality for the dashboard to adapt when a new sample is selected from the dropdown menu.

The second js file in the static folder is the bonus.js, which mainly focused on adaptive properties of the wash gauge. Like the bar chart and bubble chart, we also used the newPlot function to construct it, but the code is more complicated to construct due to having an unconventional structure compared to the biaxial structure of the other two charts. Once that was done, the app.js file could reference this function in its own code and adapt to changes in the sample the dropdown menu is currently focused on.


