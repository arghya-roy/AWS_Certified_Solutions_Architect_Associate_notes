- You can compare  Amazon QuickSight with datastudio in gcp.
- For first time you have sign up for your  Amazon QuickSight from aws.
- You can select standard option or enterprize option.
- You can connect  Amazon QuickSight with with aws account usinh SSO or active directory.
- Click on dataset.
- Tou can see some existing dataset, Click on new dataset.
- You can get many option to pick your data (data source) and integrate to  Amazon QuickSight like - Amazon Athena, EMR, Amazon Aurora, Amazon OpenSearch Service 7.7 or later, RDS, You can use files in Amazon S3, direct upload ( csv etc) etc.
- Using any of the data sources you can create dashboard.

## features -
- Serverless auto-scaling
- Broad data source support
- SPICE (super-fast, parallel, in-memory, calculation engine) ( option )
- QuickSight Mobile for iOS and Android enables you to securely get insights from your data from anywhere.
- Pay-per-use pricing.
## Spice and direct queries - 
You can use your data source in two ways
### Spice - 
- At first It picks data from data souce then keeps those inside spice.
- So data stored in spice can be used for multiple times.
- As Data stored here so it has faster processing analytical quires than direct connect.
- When data souce gets update then also have to refresh / update your spice using cron or anything else.
- **more useful for s3, csv etc.**
- More costly as compared to direct queries.
- Gets charge for store data in spice and analysis in spice.
### Direct queries -
- No need to refresh data as we must do for spice.
- only charged when you create analysis.
- **Only used for data base sources like rds, dynamodb etc**
