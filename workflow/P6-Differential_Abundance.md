# DIFFERENTIAL ABUNDANCE

Differential abundance analysis is an important component of many research studies within microbial ecology. Here we will be identifying statistically significant taxa within our dataset. These taxa identified will be those that are driving the results we saw in our alpha and beta diversity analysis. This step will involve the use of a Bash shell and Excel. 

# Getting Started in QIIME

Open your bash shell terminal, set your working directory, and load the necessary packages.

```shell
cd /work/labname/username/directory

module load python

module load qiime/1.9

module load biom-format
```

# Generating Statistical Data

For this step we will be using the `ASV_RAR.biom` file created in [Part 3](P3-Rarefaction.md#Rarefying) of the workflow as well as the [QIIME Kruskal Wallis test](https://qiime.org/scripts/group_significance.html).

We will begin by using this command to run a statistical test on our `.biom` file.

```shell
group_significance.py -i ASV_RAR.biom -m map.txt -c species -s kruskal_wallis -o DA.csv --biom_samples_are_superset --print_non_overlap
```

> [!TIP]
> | Input Arguments | Explanation |
> | --------------- | ----------- |
> | -i ASV_RAR.biom | this is your ASV table |
> | -m map.txt | this is your metadata file |
> | -c species | this is the category by which we will be run the analysis on |
> | -s kruskal_wallis | this is the statistical test |
> | -o DA.csv | this is your output file |

After running that statistical test you are going to want to go to your working directory and open the `DA.csv` file created. Select and copy all text and paste into excel. It should look something like this:

![alt text](../images/DA_1.png)

# Excel Formatting

Now what you are going to do is select all of `column A`  go to the `Data` tab up top. Then select `Text to Columns`
![alt text](../images/DA_2.png)

You are going to select `Delimited` and click `Next`, then select `Tab` as your delimiter and click `Next`, and finally keep `General` selected and click `Finish`. 



![alt text](../images/DA_3.png)

![alt text](../images/DA_4.png)

![alt text](../images/DA_5.png)



The result should look like this:
![alt text](../images/DA_6.png)

# Choosing Statistical Method

Focus on `columns C:E` they are labeled `P`, `FDR_P`, and `Bonferroni_P`, these are the statistical methods that you have to choose from. The classic P method is the least strict while Bonferroni is the most strict. We will use the values in these columns  to determine what statistical method we will use and ultimately how many of these ASVs we shall retain.

> [!Important]
> Use `a < 0.05` in determining which test statistic to use. As you can see in my example, all of my 
> statistical methods have quite a bit of significant taxa, so I will go with the strictest, 
> Bonferroni. It is up to your discretion what method you choose, however it is ultimately better to 
> have 70 ASVs that are significant using Bonferroni than 700 taxa that are significant using FDR.

In this example I will be choosing bonferonni as it the most significant and has plenty of significant ASVs. Choose your statistical method and scroll down until it is not longer significant. Insert a column between your last significant ASV and the rest of the ASVS and paint it yellow.
![alt text](../images/DA_7.png)

Now go up to the top and select your means and taxonomy and drag down continuing to select everything in those columns until you reach that yellow bar.

![alt text](../images/DA_8.png)

Copy and paste two cells to the right of your taxonomy column. Paint the column in between yellow. It should end up looking like this:
![alt text](../images/DA_9.png)


# Calculating and Graphing Differential Abundance

Now scroll down to the end of these columns (the yellow row). In the yellow row type in a function to calculate the sum of each row and drag in across. It should look something like this:

![alt text](../images/DA_10.png)

Now go up to the top again. select your column names and past them two spaces to the right again. Copy and paste the taxonomy names. Delete `_mean` from each category name. Then divide each mean by the sum calculated in the previous step. Drag down and to the right to fill in the remaining categorical variables. The function should look like the one in this photo:

![alt text](../images/DA_11.png)

Now we will use the `Text to Columns` feature again to separate out our taxonomic levels that are in our `taxonomy` column. Select the column and click the `Text to Columns` button. Keep everything the same **except** in step 2 change it from tab to semicolon:

![alt text](../images/DA_12.png)

You have every taxonomic level now down to a genus level (depending on what database you used to assign taxonomy in DADA2). Choose now the column with the taxonomic level you want and delete every other taxonomy column. Rename the column to the taxonomic level chosen. For my example I chose to do a phylum level analysis.

![alt text](../images/DA_13.png)

Now create a new sheet, type `Differential Abundance` in `cell A1` then in `cell B1` type the name of your chosen taxonomic level.

![alt text](../images/DA_14.png)

After doing that, go back to the previous sheet and select and copy all of the taxonomy data you just made, `column V` in my example.

![alt text](../images/DA_15.png)

Now go to the new sheet and paste it right under `cell B1`.

![alt text](../images/DA_16.png)

Go back to the previous sheet and choose the first categorical variable and select and copy all of the percentage values we just calculated underneath, `column R` in my example.

![alt text](../images/DA_17.png)

Now `paste as values` directly underneath `cell A1` in your new sheet.

![alt text](../images/DA_18.png)

Now insert a new column directly to the left of your differential abundance column and name it the variable you chose to do this analysis on. Then add the categorical variable name from the percentage values you just added into `cell A2` and drag down until you reach the end of all you pasted in.

![alt text](../images/DA_19.png)

Now select and copy all the phylum names and paste directly underneath the same phylum names.

![alt text](../images/DA_20.png)

Now go back to the original sheet and select and copy all the percentages of the second categorical variable and `paste as values` them under the percentages of the first one. Then name it and drag down in `column A`.

![alt text](../images/DA_21.png)

Now rinse and repeat this until you are finished. Once you are down select all of the data within this new sheet. Select the `Insert` tab and then select `PivotTable from table/range`. And select to make it on a new worksheet.

![alt text](../images/DA_22.png)

In this new sheet, select these parameters shown in the photo to make your pivot table look as presented. Then select the table as selected in the photo and paste it into a new, fourth sheet.

![alt text](../images/DA_23.png)

![alt text](../images/DA_24.png)

Then select all of the data in this sheet and go to the `Insert` tab. Select `Insert Column or Bar Chart` and choose a `100% Stacked Column`

![alt text](../images/DA_25.png)

Double click the chart you just made and go into the `Chart Design` tab. From there switch the row and column so that your bacterial taxonomy is in the legend and then properly label your chart.

![alt text](../images/DA_Results.png)

> [!Tip]
> Go to the `Page Layout` tab and change your color theme to have more access to some better color 
> palletes!

