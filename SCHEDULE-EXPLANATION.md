# Explanation of the cron Schedule

The cron expression 0 20 * * * schedules our scraper to run daily at 20:00 UTC (8:00 PM UTC). The five fields represent: minute (0), hour (20), day of month (), month (), and day of week (*), where asterisks mean 'every' occurrence. 