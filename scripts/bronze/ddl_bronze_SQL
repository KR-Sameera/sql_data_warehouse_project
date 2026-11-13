/*
===============================================================================
Stored Procedure: bronze.load_bronze
===============================================================================
Script Purpose:
    This stored procedure automates the data ingestion process for the Bronze layer 
    in the data warehouse. It performs the following actions:
    1. Truncates existing bronze tables to prepare for a fresh load (Truncate & Load).
    2. Bulk inserts raw data from CSV files (CRM and ERP sources).
    3. Tracks and prints performance metrics (execution time per table & total duration).
    4. Provides robust error handling using TRY...CATCH blocks.

Tables Loaded:
    - CRM Sources:
        * bronze.crm_cust_info
        * bronze.crm_prod_info
        * bronze.crm_sales_details
    - ERP Sources:
        * bronze.erp_cust_az12
        * bronze.erp_loc_a101
        * bronze.erp_px_cat_g1v2

Usage Example:
    EXEC bronze.load_bronze;
===============================================================================
*/
CREATE OR ALTER PROCEDURE bronze.load_bronze 
AS
BEGIN 
	DECLARE @batch_start_time DATETIME, @batch_end_time DATETIME;
	DECLARE @start_time DATETIME, @end_time DATETIME;
	
	SET @batch_start_time = GETDATE();

	BEGIN TRY 
		PRINT '================================';
		PRINT 'Loading Bronze Layer';
		PRINT '================================';

		PRINT '--------------------------------';
		PRINT 'Loading CRM Tables';
		PRINT '--------------------------------';

		-- 1. crm_cust_info
		SET @start_time = GETDATE();
		PRINT '>> Truncating Table: bronze.crm_cust_info';
		TRUNCATE TABLE bronze.crm_cust_info;

		PRINT '>> Inserting Data Into: bronze.crm_cust_info';
		BULK INSERT bronze.crm_cust_info
		FROM 'C:\Users\Sxm01\Downloads\sql-data-warehouse-project-main\sql-data-warehouse-project-main\01_datasets\source_crm\cust_info.csv'
		WITH (
			FIRSTROW = 2,
			FIELDTERMINATOR = ',',
			TABLOCK 
		);
		SET @end_time = GETDATE();
		PRINT '>> Load Duration: ' + CAST(DATEDIFF(millisecond, @start_time, @end_time) AS VARCHAR) + ' ms';
		PRINT '--------------------------------';

		-- 2. crm_prod_info
		SET @start_time = GETDATE();
		PRINT '>> Truncating Table: bronze.crm_prod_info';
		TRUNCATE TABLE bronze.crm_prod_info; 

		PRINT '>> Inserting Data Into: bronze.crm_prod_info';
		BULK INSERT bronze.crm_prod_info
		FROM 'C:\Users\Sxm01\Downloads\sql-data-warehouse-project-main\sql-data-warehouse-project-main\01_datasets\source_crm\prd_info.csv'
		WITH (
			FIRSTROW = 2,
			FIELDTERMINATOR = ',',
			TABLOCK
		);
		SET @end_time = GETDATE();
		PRINT '>> Load Duration: ' + CAST(DATEDIFF(millisecond, @start_time, @end_time) AS VARCHAR) + ' ms';
		PRINT '--------------------------------';

		-- 3. crm_sales_details
		SET @start_time = GETDATE();
		PRINT '>> Truncating Table: bronze.crm_sales_details';
		TRUNCATE TABLE bronze.crm_sales_details;

		PRINT '>> Inserting Data Into: bronze.crm_sales_details';
		BULK INSERT bronze.crm_sales_details
		FROM 'C:\Users\Sxm01\Downloads\sql-data-warehouse-project-main\sql-data-warehouse-project-main\01_datasets\source_crm\sales_details.csv'
		WITH (
			FIRSTROW = 2,
			FIELDTERMINATOR = ',',
			TABLOCK
		);
		SET @end_time = GETDATE();
		PRINT '>> Load Duration: ' + CAST(DATEDIFF(millisecond, @start_time, @end_time) AS VARCHAR) + ' ms';

		PRINT '--------------------------------';
		PRINT 'Loading ERP Tables';
		PRINT '--------------------------------';

		-- 4. erp_cust_az12
		SET @start_time = GETDATE();
		PRINT '>> Truncating Table: bronze.erp_cust_az12';
		TRUNCATE TABLE bronze.erp_cust_az12; 

		PRINT '>> Inserting Data Into: bronze.erp_cust_az12';
		BULK INSERT bronze.erp_cust_az12
		FROM 'C:\Users\Sxm01\Downloads\sql-data-warehouse-project-main\sql-data-warehouse-project-main\01_datasets\source_erp\CUST_AZ12.csv'
		WITH (
			FIRSTROW = 2,
			FIELDTERMINATOR = ',',
			TABLOCK
		);
		SET @end_time = GETDATE();
		PRINT '>> Load Duration: ' + CAST(DATEDIFF(millisecond, @start_time, @end_time) AS VARCHAR) + ' ms';
		PRINT '--------------------------------';

		-- 5. erp_loc_a101
		SET @start_time = GETDATE();
		PRINT '>> Truncating Table: bronze.erp_loc_a101';
		TRUNCATE TABLE bronze.erp_loc_a101; 

		PRINT '>> Inserting Data Into: bronze.erp_loc_a101';
		BULK INSERT bronze.erp_loc_a101
		FROM 'C:\Users\Sxm01\Downloads\sql-data-warehouse-project-main\sql-data-warehouse-project-main\01_datasets\source_erp\LOC_A101.csv'
		WITH (
			FIRSTROW = 2,
			FIELDTERMINATOR = ',',
			TABLOCK
		);
		SET @end_time = GETDATE();
		PRINT '>> Load Duration: ' + CAST(DATEDIFF(millisecond, @start_time, @end_time) AS VARCHAR) + ' ms';
		PRINT '--------------------------------';

		-- 6. erp_px_cat_g1v2
		SET @start_time = GETDATE();
		PRINT '>> Truncating Table: bronze.erp_px_cat_g1v2';
		TRUNCATE TABLE bronze.erp_px_cat_g1v2; 

		PRINT '>> Inserting Data Into: bronze.erp_px_cat_g1v2';
		BULK INSERT bronze.erp_px_cat_g1v2
		FROM 'C:\Users\Sxm01\Downloads\sql-data-warehouse-project-main\sql-data-warehouse-project-main\01_datasets\source_erp\PX_CAT_G1V2.csv'
		WITH (
			FIRSTROW = 2,
			FIELDTERMINATOR = ',',
			TABLOCK
		);
		SET @end_time = GETDATE();
		PRINT '>> Load Duration: ' + CAST(DATEDIFF(millisecond, @start_time, @end_time) AS VARCHAR) + ' ms';
		PRINT '--------------------------------';

		-- Calculate Total Batch Duration
		SET @batch_end_time = GETDATE();
		PRINT '================================';
		PRINT 'Loading Bronze Layer is Completed';
		PRINT 'Total Load Duration: ' + CAST(DATEDIFF(millisecond, @batch_start_time, @batch_end_time) AS VARCHAR) + ' ms';
		PRINT '================================';

	END TRY 
	BEGIN CATCH 
		PRINT 'Error occurred during loading bronze layer';
		PRINT 'Error Message: ' + ERROR_MESSAGE();
		PRINT 'Error Number: ' + CAST(ERROR_NUMBER() AS VARCHAR);
	END CATCH 
END
