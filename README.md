# S&P 500 Performance & Risk Analysis

This project helps to analyze the Performance and Risk-Return Profile of S&P 500 Companies to Aid Investment Decision-Making. 

This Power BI dashboard helps investors and analysts evaluate the performance, risk, and return potential of S&P 500 companies. By analyzing key metrics such as 10-year % change, 52-week % change, Beta, Profit Margin, and Yield, users can identify high-performing sectors and companies while assessing risk exposure.

Since some companies show high volatility (Beta > 1) and low profit margins, investors can make informed decisions about risk-adjusted investments. Additionally, with an average yield of X% and profit margins varying across sectors, financial professionals can optimize their portfolios by balancing risk and return potential.


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file. The data is extracted from https://www.barchart.com/
- Step 2 : Open power query editor and promote headers, change to appropriate data type, remove unwanted columns, and lastly split columns (Mostly when there is a delimiter present between required and unwanted values) if required and rename them accordingly.
- Step 3 : Some columns like Sales, Net Income and Market Capital are huge numbers. Divide (Standard operator in the Transform tab) them accordingly by an appropriate divisor to convert them into Millions/Billions.
- Step 4 : Rename the columns as Sales($M), Market Cap ($B) and Net Income ($M).
- Step 5 : Close and Apply (Power Query Editor). 
- Step 6 : Go to report view and create 7 pages, and name them as follows.

         - Intro page
         - Avg Beta & Yield
         - Avg 10 Year Change per Sector
         - Net Income Margin per Sector
         - Risk/Return Profile
         - Card
         - Tree Map
             
- Step 7 : In report view click on New Measure (Home tab), and calculate the average of 10 year % change by using the following DAX. (Average Function)

         Avg 10 Year Change = 
         AVERAGE('sp-500-index-10-31-2024'[10Y %Chg])

- Step 8 : Similarly, calculate Average Beta.

         Avg Beta = 
         AVERAGE('sp-500-index-10-31-2024'[Beta])


- Step 9 : Calculate Average Yield too.
           
         Avg Yield =
         AVERAGE('sp-500-index-10-31-2024'[Div Yield(a)])

- Step 10 : Go to Avg Beta & Yield page and plot Avg Yield vs Avg Beta Scatter plot. Drag and drop Sector into the values field. 
 The visual looks as follows: 

![Image](https://github.com/user-attachments/assets/263e3295-3cf9-4ea1-9694-077a28c14536)

  - Step 11 : Now go to "Avg 10 Year Change per Sector" page, and click on Stacked column chart in the Visualizations pane. Drag and drop sector to x-axis and Avg 10 Year Change to y-axis.
The visual will look like this: 

![Image](https://github.com/user-attachments/assets/3bef9c87-578c-4560-9541-3af02c4287a6)

- Step 12 : Now create a new measure to calculate the Net Income Margin. It is calculated as-
 Net Income margin = Net Income / Sales

DAX:

         Net Income Margin = 
         DIVIDE( SUM('sp-500-index-10-31-2024'[Net Income ($M)]),
         SUM('sp-500-index-10-31-2024'[Sales ($M)]),0) 

- Step 13 : Now go to "Net Income Margin per Sector" page. Add a Line Chart Visual. Drag and drop Sector to x-axis, Net Income Margin to y-axis.

The visual will look like this: 

![Image](https://github.com/user-attachments/assets/c932d342-7f40-4922-a97c-591c5e517114)


        
- Step 14 : Create a new Measure for Profit Margin. It is the same as Net Income margin.

         Profit Margin = [Net Income Margin]
        
 - Step 15 : Create a New measure to calculate Risk/Return Profile. It is calculated as -
Risk/Return profile = Beta/Yield.

The DAX is as follows:
       
          Risk/Ret. Profile = 
          DIVIDE(AVERAGE('sp-500-index-10-31-2024'[Beta]),
          AVERAGE('sp-500-index-10-31-2024'[Div Yield(a)]))
 
 A table with columns Full Name and Risk/ret. Profile is created in the "Risk/Return Profile" page, to analyse the Risk/Return profile of the bottom 3 companies.

In the Filters pane, select Top N filter type. Select Bottom in Show items and type 3 in the field next to it. Drag and drop Risk/Ret. profile into the By Value field.

Also add the profit Margin column to the table to help analyse the Profit Margin of these 3 companies.

![Image](https://github.com/user-attachments/assets/599dcc7e-a6ee-4171-b01d-8314e9e0e7d6)

 - Step 16 : Now in the "card" page, add a card to view the details of the company with the least Risk/Return Profile. 
 
 Select the card visual and drag & drop Full Name, Ticker Symbol, Sector and Last Price into the Fields of the visual. Similar to Step 16 filter by Bottom 1 / by Risk/Ret. Profile (by Value)

 ![Image](https://github.com/user-attachments/assets/56594a21-01c9-4470-8566-6abbac886c9c)

General Mills is the company with the least Risk/Ret. Profile.

- Step 17 : In the Tree Map page, add a Tree Map to view the Sector and Market Cap of the bottom most Company (Filter by Risk/Ret. Profile), which is General Mills.

![Image](https://github.com/user-attachments/assets/d09f11a7-b4ba-4ba2-ae87-49646ba73b88)

- Step 18 : Now go to the Intro Page and add buttons to Navigate to the rest of the pages.
Buttons are available in the Insert tab. You can choose arrow buttons and format the button as you wish. Set action to page navigation for all these buttons, and direct them to the respective pages.
Ctrl + Click on the button to navigate.

![Image](https://github.com/user-attachments/assets/034c10bc-ba8d-4757-9d8c-36bee3c5af5a)

- Step 19 : Publish Project to Power BI Service. (My Workspace)
# Snapshot of Power BI Service
![Image](https://github.com/user-attachments/assets/86e46ae5-17c5-4001-a1e3-3b367039d451)



# Insights

A multiple page report was created on Power BI Desktop & it was then published to Power BI Service.

### Following inferences can be drawn from the dashboard;

 - Computer and Technology Sector has had the highest growth (average) in the previous 10 years.
 - The Net Income of Computer and Technology Sector is higher (>20%) than other sectors.

 - The Company General Mills (Consumer Staples sector) has the least risk and returns. So the company could be a slow-growing large-cap stock or a struggling mid/small-cap stock.
