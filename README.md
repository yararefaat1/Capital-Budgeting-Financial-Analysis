# Capital-Budgeting-Financial-Analysis
This project involves creating a Power BI dashboard to evaluate the financial viability of two investment projects. Financial Metrics: NPV, IRR, and PI for both products. The dashboard enables stakeholders to make informed decisions by providing interactive and insightful financial analysis, tailored for capital budgeting strategies.
# Overview
This project is a Capital Budgeting Analysis Dashboard built using Power BI to evaluate the financial feasibility of two investment products: TC25147 and ZB95486. It provides interactive visualizations and financial metrics to assist in decision-making by analyzing cash flows, cumulative cash flows, NPV (Net Present Value), and IRR (Internal Rate of Return).

# DAX Equations Used:
1- Break-even Date: Displays the date when cumulative cash flow becomes positive.
DAX Formula:
BreakEvenDate = 
CALCULATE(
    MIN(Financials[Date]),
    FILTER(Financials, Financials[Cumulative Cash Flow] >= 0)
)

2- Payback Period: Calculates the time required to recover the initial investment.
DAX Formula:
PaybackPeriod = 
CALCULATE(
    DATEDIFF(
        MIN(Financials[Date]), 
        MAXX(FILTER(Financials, Financials[Cumulative Cash Flow] >= 0), Financials[Date]),
        YEAR
    )
)

3- Project NPV: Computes Net Present Value for each product based on discount rates.
DAX Formula:
ProjectNPV = 
SUMX(
    Financials,
    Financials[Cash Flow] / (1 + Financials[Discount Rate]) ^ Financials[Year]
)

4- Internal Rate of Return (IRR): Represents the rate of return at which NPV equals zero.
DAX Formula:
ProjectIRR = 
IRR(Financials[Cash Flow], Financials[Year])

5- Cash Flow and Cumulative Cash Flow: Displays yearly cash flows and their cumulative sum over time.
DAX Formulas:
CashFlow = SUM(Financials[Cash Flow])
CumulativeCashFlow = 
CALCULATE(
    SUM(Financials[Cash Flow]),
    FILTER(ALL(Financials), Financials[Date] <= EARLIER(Financials[Date]))
)

6- Net Present Value (NPV) Profile:Visualizes NPV at varying discount rates to analyze project sensitivity.
DAX Formula:
NPVProfile = 
SUMX(
    Financials,
    Financials[Cash Flow] / (1 + Financials[Discount Rate]) ^ Financials[Year]
)
# Visualizations
1- Cash Flow and Cumulative Cash Flow by Date and Product:
 - Combines a bar chart for cash flow and a line chart for cumulative cash flow trends.
2- Cash Flow by Year:
 - Breaks down yearly cash inflows/outflows for both products.
3- Net Present Value Profile:
 - A sensitivity chart illustrating the impact of varying discount rates on NPV.
   
# Technologies Used
 - Power BI: Data visualization and modeling.
 - DAX (Data Analysis Expressions): Custom formulas for financial metrics.
 - Data Transformation: Using Power Query to clean and preprocess financial data.
   
# How to Use
 - Clone this repository to access the Power BI file.
 - Open the file in Power BI Desktop.
 - Adjust the discount rate filter to explore different financial scenarios.
 - Review the visualizations and metrics to make data-driven investment decisions.
   
# Future Enhancements
 - Add scenario analysis for different economic conditions.
 - Include more financial metrics like ROI and ROE.
 - Automate data extraction from external financial sources.
