SELECT /* + RULE */
	df.tablespace_name AS "Tablespace"
	,df.bytes / (1024 * 1024 * 1024) AS "Size (GB)"
	,Trunc(fs.bytes / (1024 * 1024 * 1024)) AS "Free (GB)"
FROM (
	SELECT tablespace_name
		,Sum(bytes) AS bytes
	FROM dba_free_space
	GROUP BY tablespace_name
	) fs
	,(
		SELECT tablespace_name
			,SUM(bytes) AS bytes
		FROM dba_data_files
		GROUP BY tablespace_name
		) df
WHERE fs.tablespace_name = df.tablespace_name
ORDER BY 3 DESC
