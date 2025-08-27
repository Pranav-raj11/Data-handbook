### **Commonly Used Data Types**

| Data Type | Description |
| :---- | :---- |
| CHAR(size) | A FIXED length string (can contain letters, numbers, and special characters). The size parameter specifies the column length in characters \- can be from 0 to 255\. Default is 1\.  |
| VARCHAR(size) | A VARIABLE length string (can contain letters, numbers, and special characters). The size parameter specifies the maximum column length in characters \- can be from 0 to 65535 |
| INT(size) | Signed range is from \-2147483648 to 2147483647\. Unsigned range is from 0 to 4294967295\. The size parameter specifies the maximum display width |
| DECIMAL(size, d) | An exact fixed-point number. The total number of digits is specified in size. The number of digits after the decimal point is specified in the d parameter. The maximum number for size is 65\. The maximum number for d is 30\. The default value for size is 10\. The default value for d is 0\. |
| DATE | A date. Format: YYYY-MM-DD. |
| TIME(fsp) | A time. Format: hh:mm:ss.  |
| DATETIME(fsp) | A date and time combination. Format: YYYY-MM-DD hh:mm:ss. |
| YEAR | A year in four-digit format. Values allowed in four-digit format: 1901 to 2155, and 0000\. |

