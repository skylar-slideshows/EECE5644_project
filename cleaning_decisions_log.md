Cleaning Decisions

1. A copy of the raw data was made to keep the original for possible comparison later. All cleaning would happen to the copy.

2. Since the company is concerned about revenue, the cancelled orders were removed immediately. Canceled orders might as well just have not been made, as they are net 0 and make basically difference, positive or negative, to the business. They are not relevant data.

3. Revenue column was added for each order with the quantity times the price

4. "EIRE" was changed to "Ireland" for all occurrances in the country column, "RSA" to "South Africa," and "unspecified" to "MISSING." We do not remove unspecified country, since maybe somehow they didn't give that information or were on a VPN, but this is still useful order data in other ways.

5. Column names were changed to snake_case.

6. Missing descriptions and customer IDs: I was unsure if these were related to any of the other data, so a chi-square test was used at a nominal p-value of 0.05 to detect if missing descriptions were due to some confounding factor visible in the relationship to other columns, or if it was unrelated to other data and was random noise that provides no information. Both highest p values were found to be below 0.05, so we reject the null hypothesis that this is due to random chance. Therefore we keep all missing description and missing customer ID orders, since they contain some relationship or pattern to the other data that is not likely to have happened by chance, that future ML processing may help explain.

7. Why was invoice_number column deleted: invoice number is not relevant to my analysis, and it doesn't really mean anything in the "trends" the business questions are asking about. They are for the company's internal use to track orders, and they are unrelated to who the customer actually is; they could be completely random as far as we are concerned. We have already deleted the canceled orders, so these have no more useful data. I thought initially that "description" could also be removed, reasoning that it was redundant with stock code. However, we see with nunique above that there are more unique descriptions than stock codes, so they are not interchangable or 1-to-1. Therefore, there is some more complex relationship between stock code and description so both are kept.

8. Removing rows with data that doesn't make sense: Quantity = 0 means a non-sale, so we remove rows with this. Price <= 0 doesn't make sense, and stock code "POST" reports postage cost, which I assume the company is not "selling" as a product like everything else. All these types of rows are removed.