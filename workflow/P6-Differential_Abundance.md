# Differential Abundance

Differential abundance analysis is an important component of many research studies within microbial ecology. Here we will be identifying statistically significant taxa within our dataset. These taxa identified will be those that are driving the results we saw in our alpha and beta diversity analysis. This step will involve the use of a Bash shell and Excel. 

# Getting Started in QIIME

Open your bash shell terminal, set your working directory, and load the necessary packages.

```shell
cd /work/labname/username/directory

module load python

module load qiime/1.9

module load biom-format
```

# Statistical Analysis

For this step we will be using the `ASV_RAR.biom` file created in [Part 3](P3-Rarefaction.md#Rarefying) of the workflow as well as the [QIIME Kruskal Wallis test](https://qiime.org/scripts/group_significance.html).

We will begin by using this command to run a statistical test on our `.biom` file.

```shell
group_significance.py -i ASV_RAR.biom -m map.txt -c diet -s kruskal_wallis -o DA.csv --biom_samples_are_superset --print_non_overlap
```

> [!TIP]
> | Input Arguments | Explanation |
> | --------------- | ----------- |
> | -i ASV_RAR.biom | this is your ASV table |
> | -m map.txt | this is your metadata file |
> | -c diet | this is the category by which we will be run the analysis on |
> | -s kruskal_wallis | this is the statistical test |
> | -o DA.csv | this is your output file |

After running that statistical test you are going to want to go to your working directory and open the `DA.csv` file created. Select and copy all text and paste into excel. It should look something like this:

To be continued