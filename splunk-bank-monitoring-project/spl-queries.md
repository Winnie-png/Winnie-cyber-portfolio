# Splunk Bank Monitoring Project — All SPL Queries

# 1. Failed Login Attempts
index=main action="login_failed" | timechart count

# 2. Most Active Users
index=main action="login" | stats count by user | sort -count

# 3. High-Value Transactions
index=main action="transaction" amount>10000 | timechart sum(amount)

# 4. Suspicious IP Activity
index=main action="login" | stats count by user, ip_address | where count>5

# 5. Data Verification — Check that all events are ingested
source="bank_logs.csv"

# 6. Search Tab Check — Ensure dashboard queries return results
index=main OR index=default | head 20
