# Salary Survey 2021 (Data-Cleaning)
> This survey was conducted by [Ask a Manager](https://www.askamanager.org/), in order to get some real-world information about what jobs pay, with no need to ask people directly, as it gets weird to do so.
>
> You can have a quick view on [data](https://docs.google.com/spreadsheets/d/1IPS5dBSGtwYVbjsfbaMCYIWnOuRmJcbequohNxCyGVw/edit?resourcekey#gid=1625408792) before *cleaning*.

**This project aims to go through this messy data, and figure out how to clean it correctly** .  
(n.b. *This is my first data cleaning project*)

***

### What was done in this project:  
- Fixing attributes' data type
- Figuring out the root cause of the problem
- Imputing missing values
    - Most missing data *do not exist*
    - No-way to figure out not existing data, as it is a *survey data*
- Fixing several columns' inconsistencies as much as is feasible
    - Removing extra-spaces
    - Normalizing into lowercase
    - NLP techniques (Removing stopwords, Lemmatization)
    - Mapping values using keywords (extracted using **Excel**)
- Merging relative columns
- Analyzing several problems, and trying to fix them


### Problem's root cause:
> The survey answers ***were based on open-ended questions***, so there was quite the room for numerous different values for each attribute even though they could be broken into much more less categories.


### Our cleaning results:
- Straightforward, usable labels
- Correct data types
- Imputing ~85k missing values
- Fixed attributes' inconsistencies
    - *'job_title'*: ~ 2.5k false-unique cleaned
    - *'industry'*: ~ 600 false-unique cleaned & remapped
    - *'updated_currency'*: ~ 90 false-unique cleaned & remapped, 2 relevant columns merged
    - *'workin_country'*: ~ 150 false-unique cleaned & remapped
    

### Quality issues:
- *'job_title'*
   - Looks like 11.7k unique job titles ***was not that unreasonable*** according to its huge number. Titels are associated with its career progression (i.e *entry-level* Data Analyst, *Senior* Data Analyst), which intuitively affects salary. Mapping them into one category could make a huge bias on data's most important objective, salaries, compared to its current errors.
   - While trying to impute *'industry'* missing values according to associated *'job_title'*, but found out that common job titels are associated with different *'industry'* values, so such imputing is no better than being missing.
- *'industry'*
   - Intuitivly, taking all survey specified industries into account of new categories is a bad decision, maybe some of them which is relatively close to other false-unique categories (i.e Education). Also, there is no way to clean all dirty industries, but maybe brake them down into a smaller number.
   - After examining the whole 980 unique values using pivot table, custom sorting the pivot data (Descending count -> A-Z industry), and Find tool, found out 19 industry categories to map values to, that may cause fixing ~400 unique values.
   - Undeniably that there are other values need cleaning, but they need manual cleaning, which is a huge effort compared to cleaning benefits.
- *'other_currency'*
   - Even though USD was in the dropbox, some people chose other and wrote USD, other came to be creative and wrote american dollars.
   - Similar problems occured with other currencies (were in the dropbox, or not), but they can be handled easily.
   - After a 40-min search for currencies (where I picked up some great knowledge ^^), found 18 currencies to be mapped to using list of keywords.
- *'workin_country'*
   - After 60-min of searching and extracting keywords in country unique values, I found that many unique values are dirty due to additional info (i.e 'i am located in canada but i work for a company in the us', instead of just 'usa'), and different forms of writing usa (i.e 'u.s.a', 'u.s.a.', 'uniter statez', 'the united states').
   - Not all false-unique values could be mapped as I search with substring, and it may damage other clean data causing bigger problems.
   - Although made an explicit replace operation for 'us' (specifically as it exsited in ~600 rows), as searching with substring 'us' would map false values, causing more dirty data.


***


### Files in repo:
`Ask A Manager Salary Survey 2021 (Form Responses)`: Original Dataset  
`Cleaned_Survey`: Dataset after being cleaned  
`Salary Survey 2021 (Data Cleaning)`: The project notebook
