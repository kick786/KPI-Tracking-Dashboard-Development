// Load data from your data source (e.g., SQL database, Excel file, etc.)
source = <Your Data Source>,

// Define KPIs
KPI1 = CALCULATE(SUM('source'[Metric1])),
KPI2 = CALCULATE(SUM('source'[Metric2])),
KPI3 = CALCULATE(SUM('source'[Metric3])),

// Create a table with KPIs
KPI_Table = DATATABLE(
    "KPI", STRING, "Value", DOUBLE,
    {
        {"KPI 1", KPI1},
        {"KPI 2", KPI2},
        {"KPI 3", KPI3}
    }
),

// Define visualization settings
KPI_Table_Visual = SELECTCOLUMNS(KPI_Table, "KPI", "Value"),

// Create the KPI dashboard
KPI_Dashboard = 
    Page {
        GroupBox {
            GroupBox.Header { Text = "KPI Tracking Dashboard" },
            GroupBox.Content {
                Grid {
                    Columns = 2,
                    Content = {
                        Card {
                            CardTitle = "KPI 1",
                            Data = KPI1
                        },
                        Card {
                            CardTitle = "KPI 2",
                            Data = KPI2
                        },
                        Card {
                            CardTitle = "KPI 3",
                            Data = KPI3
                        }
                    }
                }
            }
        }
    }

// Render the dashboard
EVALUATE KPI_Dashboard
