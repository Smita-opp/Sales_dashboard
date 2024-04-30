# Sales-Dashboard

# Dashboard Link- https://app.powerbi.com/groups/me/reports/f463a72a-e6f6-4b80-8929-d346ee0b1819/ReportSection6af363d1f10528b4b2a4?experience=power-bi

## Problem Statement

The Small retailer company  is facing issues in managing and analyzing their sales data. The sales team is struggling to make sense of the data and they do not have a centralized system to manage and analyze the data. The management is unable to get accurate and up-to-date sales reports, which is affecting the decision-making process.

This dashboard helps to understand, manage, and analyze their sales data. Through this dashboard company knows the sales patterns, cost, and profit. Through different views, they get to know the entire sales pattern, thus they can improve their Sales by identifying this area. 


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a excel file.
- Step 2 : Open Power query editor, then Promote the 1st row as headers and remove the unwanted column to reduce the size of the data set. 
- Step 3 : In view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 4 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 5 : It was observed that in none of the columns errors & empty values were present.
- Step 6 : In the report view, under the view tab, theme was selected.
- Step 7 : Date table was created with the help of CALENDARAUTO() Function.
- Step 8 : Visual filters (Slicers) were added for four fields named "Sales Type", "payment mode", "Year" & "Month".
- Step 9 : 4 card visuals were added to the canvas, one representing Total Sales, and another representing the Profit. The remaining two represent profit % and Quantity
 - Step10: Field parameters allow users to dynamically change the measures or dimensions being analyzed within a report. Parameter was created by using Sale, Profit, and profit % fields. This feature can helpreport readers explore and customize the analysis of the report by selecting the different measures or dimensions they're interested in. 
- Step 11: A bar chart was also added to the report design area representing the Product code-wise Sales, Profit , and Profit %.  
- Step 12: A clustered column chart was added to analyse the month-wise transaction and an Area Chart was added for daywise Sale analysis.
- Step  13:  Pie charts were added to represent the data, a circle to represent the wholesale, and slices of that circle, or “pie”, to represent the Sale types and Payment modes that compose the wholesale. The treemap represents certain categories within a selected dimension.
 
- Step 14: In the report view, under the insert tab, two one boxes were added to the canvas, to written Dashboard name.
     
- Step 15 : New measure was created to find total sale.

Following DAX expression was written for the same,
        
Sale = CALCULATE(
                SUM('Master Data.'[TOTAL SELING PRICE]))
                        
        
A card visual was used to represent Total Sale


![image](https://github.com/Smita-opp/Test/assets/159506053/cee68c83-300e-4f5b-9b31-dc6651dee64e)
        
 - Step 16 : New measure was created to find  profit,
 
 Following DAX expression was written to Profit,
 
         Profit = VAR 
         Sale=CALCULATE(
                        SUM('Master Data.'[TOTAL SELING PRICE]))
                         VAR 
                            cost=CALCULATE(
                                SUM('Master Data.'[TOTAL BUYING PRICE]))
                                RETURN
                                     Sale-cost
 
 A card visual was used to represent this profit
 
 Snap of Profit.
![image](https://github.com/Smita-opp/Test/assets/159506053/453faa0c-fc3c-4fcc-b6e6-5c8256a8ae25)
 
 
 
 - Step 17 : New measure was created to calculate Profit %
 
 Following DAX expression was written to find total distance,
 
         Profit% = VAR 
             cost=CALCULATE(
                    SUM('Master Data.'[TOTAL BUYING PRICE]))
                        RETURN
                          [Profit]/cost    
 A card visual was used to represent this Profit %.
 
 
![image](https://github.com/Smita-opp/Test/assets/159506053/d49e9861-0741-4e54-919d-faeb3afd07e2)

- Step 17 : New measures was created to find the Top product & Top Category
 
 Following DAX expression was written to find Top Product & Category,
 
        Top product = FIRSTNONBLANK(TOPN(1,VALUES('Master Data.'[PRODUCT]),[Sale]),1)
          Top category = FIRSTNONBLANK(
                      TOPN(1,
                            VALUES('Master Data.'[CATEGORY]),
                                [Sale])
                                
                                ,1)


 
 - Step 18 : The report was then published to Power BI Service.
 
# Snapshot of Dashboard (Power BI Service)

![image](https://github.com/Smita-opp/Test/assets/159506053/3858ad00-5e46-4d69-80c1-859c24e2f26c)
 
 # Report Snapshot (Power BI DESKTOP)

![image](https://github.com/Smita-opp/Test/assets/159506053/6cc2eb64-da49-4afa-9b5b-8636e203c97f)

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Total Number of Sale = Rs.3,81,856 

   Total Profit = Rs.49,352

   Profit % = 14.84%

   Quantity=4280

           
### [2] With Different Sale type

    a) Direct Sale
      Sale-199824
      Profit-27914
      Profit %-16.24 %

    b) Online
      Sale-126563
      Profit-14760
      Profit %-13.20 %

    c) Wholesaler
      Sale-55460
      Profit-6678
      Profit %-13.69 %
   
   
  
  ### [3] Top selling Product
          Product30
          Top Category
          Category5.

Report page Two:

Sales Growth Analysis:

# Snapshot of Dashboard (Power BI Service)

![image](https://github.com/Smita-opp/Test/assets/159506053/dde9188a-f601-432d-b0b9-2a76e54a9ab2)


The main DAX Functions used in the reports are mentioned below.

1. Sales Compaion for different dates.

Sale = CALCULATE(
                SUM('Master Data.'[TOTAL SELING PRICE]))
                        


Salecomp = (CALCULATE([Sale],
               USERELATIONSHIP('Date Comparision'[Date],
                     'Master Data.'[DATE]),
                          REMOVEFILTERS('Date')))

2. Profit Coparision.
Profit = VAR 
         Sale=CALCULATE(
                        SUM('Master Data.'[TOTAL SELING PRICE]))
                         VAR 
                            cost=CALCULATE(
                                SUM('Master Data.'[TOTAL BUYING PRICE]))
                                RETURN
                                     Sale-cost

 Profit comp = (CALCULATE([Profit],
               USERELATIONSHIP('Date Comparision'[Date],
                     'Master Data.'[DATE]),
                          REMOVEFILTERS('Date')))


3.Profit Growth
   Profit Growth = [Profit comp]-[Profit]

4. Sales Growth
   Sale Growth = [Salecomp]-[Sale]

5.Sales Growth
Sale Growth% = [Sale Growth]/[Salecomp]

6.Profit Growth
  
Profit Growth% = DIVIDE([Profit Growth],[Profit])
            
