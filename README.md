# Optimizing Supplier Quality and Downtime Reduction through Data Analytics for Enterprise Manufacturers Limited

# Project Overview:
## Background:
Enterprise Manufacturers Limited is on a mission to revamp their procurement processes and ensure top-notch quality of raw materials from their various vendors across different plants. With no standardized procurement system in place, the company has been facing issues with vendor performance, plant operations, and process efficiency. However, the company has recently collected valuable data on material, vendor, plant location, defect quantity, and downtime caused by defective materials.

The main goal of this project is to dive into the consolidated data and extract crucial insights regarding supplier quality and operational downtime. By making use of Power BI for data visualization, the project aims to provide actionable insights that will empower management to make well-informed decisions, leading to increased revenue, reduced costs, and enhanced process efficiency

## Objectives:
1. Identify Poor-Performing Vendors and Plants: Analyze which vendors and plants are associated with the highest quantity of defective materials and the most downtime, to help focus improvement efforts.
2. Vendor-Material Analysis: Determine if specific combinations of vendors and materials consistently lead to poor performance, enabling more strategic procurement decisions.
3. Plant-Vendor Relationship: Identify how the same vendors and materials perform across different plants, and pinpoint any discrepancies in performance that could impact efficiency.
4. Downtime Impact Assessment: Analyze the value of downtime caused by defective materials, and identify the vendors and plants that contribute the most to operational inefficiencies and cost overruns.
5. Propose Solutions: Provide data-driven recommendations for improving procurement processes, including identifying poor-performing vendors, improving supplier relationships, and minimizing downtime, ultimately driving cost savings and operational improvements.
   
## Key Questions:
Here are the burning questions that will guide the project and meet the expectations of the company stakeholders:

- Which vendors and plants are causing the greatest defect quantity?
- Which vendors and plants are causing the greatest downtime?
- Are there specific combinations of materials and vendors that perform poorly?
- Are there specific combinations of vendors and plants that result in poor performance?
- How do the same vendor and material perform across different plants?

# Data Description 
The dataset consists of 5,226 rows and 9 columns. Here's a breakdown of the columns:

1. Date: The date of recording defects and downtime
2. Vendor: The supplier of the materials
3. Plant Location: The geographical location of the production facility
4. Category: The classification of the materials supplied
5. Material Type: The type of material supplied
6. Defect Type: The severity of the defect in the material (e.g., Impact, No Impact, Rejected)
7. Defect: A summary of the flaw in the material
8. Total Defect Quantity: The quantity of defective material received
9. Total Downtime Minutes: The duration of plant inactivity due to defective materials
    
# Data Normalization:
The dataset was in good shape, but I optimized it by creating dimension tables and a fact table for better performance, organization, and analysis.

The dimensions table held categorical data which helped to describe the business processes or events which will be represented in the fact table. The first step involved duplicating the original table, Supplier Quality, six times. Each of the duplicated tables was uniquely renamed using identifiers such as Vendor, Plant, Category, Material Type, Defect, and Defect Type. Then, in the Vendor table, the column relevant to the dimension was selected using the choose-columns feature. Thereafter, duplicates were removed using the remove-duplicates feature to retain unique data. Finally, the primary key was created by using the add-column feature to add an index column starting from 1. The primary key was renamed to the ID version of the categorical column, such as VendorID. The data type was changed to the text data type. This process was repeated in the Plant, Category, Material Type, Defect, and Defect Type tables. 

After the successful creation of the dimension tables, the final stage in this data normalization step is to create the fact table. The fact table is the central table that contains quantitative data about business processes. They are typically numeric values and contain foreign keys that link to dimension tables. The first step in the creation of the fact table is to use the merge-queries-as-new feature to merge the Supplier Quality table with the Vendor table. In the merge tab, the Vendor column was selected on both tables and joined using the inner join kind. The new merged query was renamed as Supplier Fact. The new column added to the fact table was expanded to select the foreign key, VendorID. This process was repeated by using the merge-queries feature to merge the Plant, Category, Material type, Defect, and Defect type to the fact table. The foreign keys were changed to the text data type.  Finally, only the following columns were retained: Date, Total defect quantity, Total downtime minutes, and the columns associated with the foreign keys.

The date table was created using a DAX measure for time intelligence calculations and the date column was marked as a date table using table tools. The date table is an important step for enabling time intelligence calculations, such as month-over-month (MoM), year-over-year (YoY), or cumulative totals. 

# Data Modelling:
The data modeling process involved connecting primary keys in the dimension tables to foreign keys in the fact table using the one-to-many cardinality to achieve a star schema model. 

# Descriptive Analysis:
## Let’s first draw some visuals to help us deep dive into the data

### When it comes to analyzing supplier data, Key Performance Indicators (KPIs) are crucial for assessing supplier performance. So, what specific KPIs should we focus on in this analysis?

![KPI](https://github.com/user-attachments/assets/5f01897d-c92f-4fb5-ad6f-0fc055b81bda)

**Enterprise Manufacturers Limited** faced significant operational challenges in **2018 and 2019**, recording approximately 2.60 billion defective units and 215,800 hours of downtime. The impact of these issues resulted in substantial losses, with an estimated cost of $2.16 million for downtime alone, equating to a loss of $10 for every hour of operational downtime.

The data strongly suggests that tackling both defects and downtime could lead to significant cost savings and an overall improvement in efficiency. By reducing downtime and defect rates, Enterprise Manufacturers Limited has the potential to optimize production and recoup lost revenue.

**Recommendation:** It's essential to prioritize strategies aimed at reducing downtime through enhanced equipment maintenance and process optimization, while also concentrating on quality control to lower defect rates. 


### Having identified the KPIs, which vendors and plants are performing poorly?
  
![Defect Quantity 1](https://github.com/user-attachments/assets/cf05c29e-c8ea-45a6-8e42-d3525bf8a04d). ![Defect Quantity 2](https://github.com/user-attachments/assets/6972f6e6-4466-4515-8cc7-b912f864fef1)

The analysis reveals that the top three underperforming vendors in terms of **defect quantities** are Yombu, Avamm, and Meejo, contributing 15.1M, 14.7M, and 14.2M defective units, respectively. On the plant side, Hingham, Charles City, and Twin Rocks lead in poor performance with 100M, 99M, and 97M defect units.

![Downtime Hours by Vendor](https://github.com/user-attachments/assets/e01414e0-1043-404a-8003-347374a41212)![Downtime Hours by Plant Location](https://github.com/user-attachments/assets/eef0167d-ac14-4500-bc2b-dff505e434a7)

In terms of **downtime**, Avamm, Izio, and Meetz top the list of vendors with 1,165, 1,144, and 1,134 downtime hours, while Riverside, Charles City, and Twin Rocks are the worst-performing plant locations, with 8.6K, 8.3K, and 8.0K downtime hours. These downtime hours result from various operational inefficiencies, not limited to defect quantity.

**Recommendation:** Focus on improving vendor management and plant-level operations, especially in defect control and downtime reduction. To reduce both defect quantities and downtime, a targeted approach should be taken to address inefficiencies at the highest-impact vendors and plant locations. Implementing stricter quality controls and enhanced maintenance protocols at these sites can mitigate losses and improve overall operational performance


### Considering the singular impact of either vendor or the plant in isolation when analyzing downtime hours provides useful insights, but it may not present the full picture of operational inefficiencies. I'll have to consider specific plant and vendor combinations that consistently lead to poor performance to ascertain root causes. Also, do certain vendor and material combinations impact efficiency?

![Vendor-Material](https://github.com/user-attachments/assets/3a4927c2-a311-48ee-9934-14c08030d780)![Vendor Plant](https://github.com/user-attachments/assets/e6ada421-59f8-44dc-b939-17528f7c28d4)

The combination of **Edgelab and Raw Materials** emerged as the leading source of inefficiencies, with 6,350,491 defective units, 292.85 hours of downtime, and a downtime cost of $2,928.50. Similarly, the pairing of **Yombu and Prescott plant** recorded 3,215,078 defective units, 195.63 hours of downtime, and a downtime cost of $1,956.33.

These findings indicate that certain vendor-material and vendor-plant combinations are significantly contributing to defects and downtime, leading to increased costs and reduced productivity. Tackling these inefficiencies could result in substantial operational improvements.

**Recommendation:** Prioritize enhancing the quality control process at Edgelab’s raw material stage and streamline the operations between Yombu and Prescott. By addressing these specific high-impact areas, the company can minimize defects and reduce downtime, leading to a significant reduction in associated costs.


### Let's not forget the material analysis section. What's the most common defect flaw? Which type of material have the highest defect quantity? And which classification does the material fall under?

![Category](https://github.com/user-attachments/assets/3cd3a92f-6016-4b06-af5e-12b89970f900)![Material Type](https://github.com/user-attachments/assets/0334a538-d1db-4aec-81bc-a95735826da3)![Defect](https://github.com/user-attachments/assets/72657f2f-9bf8-45a2-816d-b486ac0daf54)

The **Bad Seams defect** has emerged as the leading cause of production inefficiencies, resulting in 146 million defective units. Among material type, **Raw Materials** contribute to the highest defect quantity with 0.77 billion units. While the **Mechanicals category** lead other categories with a 0.82 billion defective units.

These figures highlight critical problem areas in both materials and mechanical processes, significantly impacting product quality. The high defect rates across these categories are driving up costs and reducing overall operational efficiency.

**Recommendation:** Prioritize addressing the Bad Seams defect by refining production techniques and tightening quality control. Additionally, focus on improving the quality of Raw Materials and Mechanical components through better vendor management and enhanced process oversight to boost overall performance.


### Finally, various factors can result into downtime, as stated earlier, however, what's the highest value of downtime caused by defective materials? 

![Worst Performance](https://github.com/user-attachments/assets/b71c8855-a84f-4959-b0e0-bee7fc2d11b2)

By vendor, **Avamm, Meejo, and Yombu** lead in downtime caused by defective materials, recording 1,164.82, 778.32, and 763.62 hours, respectively. On the plant side, **Charles City, Twin Rocks, and Hingham** stand out with the highest downtimes due to defective materials, with 8,283.10, 8,000.70, and 7,317.08 hours, respectively.

These findings indicate that both vendors and plants are experiencing substantial downtime linked to defective materials, resulting in significant operational delays and cost inefficiencies. Addressing these issues at the vendor and plant levels will be key to improving production flow and minimizing losses.

**Recommendation**: Focus on improving the quality of materials supplied by **Avamm, Meejo, and Yombu** to reduce downtime. Additionally, streamline operations at **Charles City, Twin Rocks, and Hingham** by enhancing defect detection and resolution processes, which will help lower the downtime caused by material defects and improve overall efficiency.

# Recommendation:
