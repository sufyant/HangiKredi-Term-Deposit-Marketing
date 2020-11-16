# Next Campaign Strategy
<a id="4"></a>
<img src="https://media.giphy.com/media/l46Cy1rHbQ92uuLXa/giphy.gif">

## Months of Marketing Activity
<a id="4.1"></a>
We saw that the the month of highest level of marketing activity was the month of **May**. However, this was the month that potential clients tended to reject term deposits offers. For the next marketing campaign, it will be wise for the bank to focus the marketing campaign during the months of **October and March** (December should be under consideration because it was the month with the lowest marketing activity, there might be a reason why december is the lowest.)

month = df.groupby('month')[['y']].sum().reset_index().rename(columns={'y':'y_yes'})
month['total_call'] = df.groupby('month')[['y']].count().values
month['rate'] = month['y_yes']/month['total_call']
month.sort_values('rate',inplace=True,ascending=False)
month

sns.catplot(x="month", hue='y', data=df, kind="count",height=10);

## Seasonality
<a id="4.2"></a>
Potential clients opted to suscribe term deposits during the seasons of **winter** and **spring**. The next marketing campaign should focus its activity throghout these seasons.

df2['y'] = df2['y'].apply(lambda x: 1 if x=='yes' else 0)

df2.loc[df["month"] == 'dec', 'season'] = 'winter'
df2.loc[df["month"] == 'jan', 'season'] = 'winter'
df2.loc[df["month"] == 'feb', 'season'] = 'winter'

df2.loc[df["month"] == 'mar', 'season'] = 'spring'
df2.loc[df["month"] == 'apr', 'season'] = 'spring'
df2.loc[df["month"] == 'may', 'season'] = 'spring'

df2.loc[df["month"] == 'jun', 'season'] = 'summer'
df2.loc[df["month"] == 'jul', 'season'] = 'summer'
df2.loc[df["month"] == 'aug', 'season'] = 'summer'

df2.loc[df["month"] == 'sep', 'season'] = 'fall'
df2.loc[df["month"] == 'oct', 'season'] = 'fall'
df2.loc[df["month"] == 'nov', 'season'] = 'fall'

sns.catplot(x="season", hue='y', data=df2, kind="count",height=10);

season = df2.groupby('season')[['y']].sum().reset_index().rename(columns={'y':'y_yes'})
season['total_call'] = df2.groupby('season')[['y']].count().values
season['rate'] = season['y_yes']/season['total_call']
season.sort_values('rate',inplace=True,ascending=False)
season

## Campaign Calls
<a id="4.3"></a>
A policy should be implemented that states that no more than 4 calls should be applied to the same potential client in order to save time and effort in getting new potential clients. Remember, the more we call the same potential client, the likely he or she will decline to open a term deposit.

sns.catplot(x="campaign", hue='y', data=df2, kind="count",height=10);

campaign = df2.groupby('campaign')[['y']].sum().reset_index().rename(columns={'y':'y_yes'})
campaign['total_call'] = df2.groupby('campaign')[['y']].count().values
campaign['rate'] = campaign['y_yes']/campaign['total_call']
campaign.sort_values('rate',inplace=True,ascending=False)
campaign

## Age Category
<a id="4.4"></a>
The bank's next marketing campaign should target potential customers between the ages of **20 and 35**. The chance of this category to be exposed to time deposits is **8.5%**. It would be great for the next campaign for the bank to address this categorie and therefore increase the likelihood of more time deposits suspicion.

def age_class(df):
        
    df.loc[df['age'] <= 20, 'AGE_CLASS'] = 'under20'
    
    df.loc[(df['age'] > 20) & (df['age'] <= 35), 'AGE_CLASS'] = '20-35'
    
    df.loc[(df['age'] > 35) & (df['age'] <= 50), 'AGE_CLASS'] = '35-50'
        
    df.loc[(df['age'] > 50) & (df['age'] <= 60), 'AGE_CLASS'] = '50-60'
   
    df.loc[df['age'] > 60, 'AGE_CLASS'] = '60+'

age_class(df2)

sns.catplot(x="AGE_CLASS", hue='y', data=df2, kind="count",height=10);

age = df2.groupby('AGE_CLASS')[['y']].sum().reset_index().rename(columns={'y':'y_yes'})
age['total_call'] = df2.groupby('AGE_CLASS')[['y']].count().values
age['rate'] = campaign['y_yes']/campaign['total_call']
age.sort_values('rate',inplace=True,ascending=False)
age

## Occupation
<a id="4.5"></a>
Not surprisingly, potential clients that were students or retired were the most likely to suscribe to a term deposit. Retired individuals, tend to have more term deposits in order to gain some cash through interest payments. Remember, term deposits are short-term loans in which the individual (in this case the retired person) agrees not to withdraw the cash from the bank until a certain date agreed between the individual and the financial institution. After that time the individual gets its capital back and its interest made on the loan. Retired individuals tend to not spend bigly its cash so they are morelikely to put their cash to work by lending it to the financial institution. Students were the other group that used to suscribe term deposits.

job = df2.groupby('job')[['y']].sum().reset_index().rename(columns={'y':'y_yes'})
job['total_call'] = df2.groupby('job')[['y']].count().values
job['rate'] = job['y_yes']/job['total_call']
job.sort_values('rate',inplace=True,ascending=False)
job

## House Loans and Balances
<a id="4.6"></a>
Potential clients in the low balance and no balance category were more likely to have a house loan than people in the average and high balance category. What does it mean to have a house loan? This means that the potential client has financial compromises to pay back its house loan and thus, there is no cash for he or she to suscribe to a term deposit account. However, we see that potential clients in the average and hih balances are less likely to have a house loan and therefore, more likely to open a term deposit. Lastly, the next marketing campaign should focus on individuals of average and high balances in order to increase the likelihood of suscribing to a term deposit.

loan = df2.groupby('loan')[['y']].sum().reset_index().rename(columns={'y':'y_yes'})
loan['total_call'] = df2.groupby('loan')[['y']].count().values
loan['rate'] = loan['y_yes']/loan['total_call']
loan.sort_values('rate',inplace=True,ascending=False)
loan

## Target individuals with a higher duration (above 254)
<a id="4.7"></a>
Target the target group that is above average in duration, there is a highly likelihood that this target group would open a term deposit account. The likelihood that this group would open a term deposit account is at 46% which is pretty high. This would allow that the success rate of the next marketing campaign would be highly successful.

df2.corr()

df['duration'].mean()

***
#### By combining all these strategies and simplifying the market audience the next campaign should address, it is likely that the next marketing campaign of the bank will be more effective than the current one.


 
