with T5 as
(
  with T4 as
(
select (min(T3."Due_Date")) as "DPD", T3."User_ID" as users, T3."Due_Date", (sum(T3."outstandingloan")) as "outstandingloan1" from
(
select (T0."Outstanding_Balance" + T0."Principal_Payable") as "outstandingloan", T0."User_ID", T0."Due_Date" from public.emi_schedule as T0, public.order_details as T1
where
T0."EMI_Amount" is not null and
T0."Loan_Status" != 'cancelled' and
(T0."Payment_Status" = 'pending'  or (T0."Payment_Status" = 'paid' and T0."Paid_Date" > '2017-01-01')) and
T0."Order_ID" = T1."order_id" and
T1."order_status" != 'refunded' and
T1."order_status" != 'refundReceived' and
T0."Due_Date" < current_date
  


  ) as T3
group by T3."User_ID",T3."Due_Date"
)
  select dpd_range,  sum from(
select '0-30' as dpd_range,  sum(outstandingloan1) from T4 where "DPD" = '2017-01-05'
group by dpd_range
UNION
select '30-60' as dpd_range, sum(outstandingloan1) from T4 where "DPD" = '2016-12-05' 
group by dpd_range
UNION
select '60+' as dpd_range, sum(outstandingloan1) from T4 where "DPD" <= '2016-11-05'
group by dpd_range

order by dpd_range) A),
T6 as
(
  with T4 as
(
select (min(T3."Due_Date")) as "DPD", T3."User_ID" as users, T3."Due_Date", (sum(T3."outstandingloan")) as "outstandingloan1" from
(
select (T0."Outstanding_Balance" + T0."Principal_Payable") as "outstandingloan", T0."User_ID", T0."Due_Date" from public.emi_schedule as T0, public.order_details as T1
where
T0."EMI_Amount" is not null and
T0."Loan_Status" != 'cancelled' and
(T0."Payment_Status" = 'pending' or (T0."Payment_Status" = 'paid' and T0."Paid_Date" > '2017-01-01')) and
T0."Order_ID" = T1."order_id" and
T1."order_status" != 'refunded' and
T1."order_status" != 'refundReceived' and
T0."Due_Date" < current_date
  


  ) as T3
group by T3."User_ID",T3."Due_Date"
)
  select dpd_range,  count from(
select '0-30' as dpd_range,  count(users) from T4 where "DPD" = '2017-01-05' and "outstandingloan1" <= 1000
group by dpd_range
UNION
select '30-60' as dpd_range, count(users) from T4 where "DPD" = '2016-12-05' and "outstandingloan1" <= 1000
group by dpd_range
UNION
select '60+' as dpd_range, count(users) from T4 where "DPD" <= '2016-11-05' and "outstandingloan1" <= 1000
group by dpd_range

order by dpd_range) A),
T7 as 
(
  with T4 as
(
select (min(T3."Due_Date")) as "DPD", T3."User_ID" as users, T3."Due_Date", (sum(T3."outstandingloan")) as "outstandingloan1" from
(
select (T0."Outstanding_Balance" + T0."Principal_Payable") as "outstandingloan", T0."User_ID", T0."Due_Date" from public.emi_schedule as T0, public.order_details as T1
where
T0."EMI_Amount" is not null and
T0."Loan_Status" != 'cancelled' and
(T0."Payment_Status" = 'pending' or (T0."Payment_Status" = 'paid' and T0."Paid_Date" > '2017-01-01')) and
T0."Order_ID" = T1."order_id" and
T1."order_status" != 'refunded' and
T1."order_status" != 'refundReceived' and
T0."Due_Date" < current_date
  
  ) as T3
group by T3."User_ID",T3."Due_Date"
)
  select dpd_range,  count from(
select '0-30' as dpd_range,  count(users) from T4 where "DPD" = '2017-01-05' and ("outstandingloan1" between 1001 and 7000)
group by dpd_range
UNION
select '30-60' as dpd_range, count(users) from T4 where "DPD" = '2016-12-05' and ("outstandingloan1" between 1001 and 7000)
group by dpd_range
UNION
select '60+' as dpd_range, count(users) from T4 where "DPD" <= '2016-11-05' and ("outstandingloan1" between 1001 and 7000)
group by dpd_range

order by dpd_range) A),
T8 as
(
  with T4 as
(
select (min(T3."Due_Date")) as "DPD", T3."User_ID" as users, T3."Due_Date", (sum(T3."outstandingloan")) as "outstandingloan1" from
(
select (T0."Outstanding_Balance" + T0."Principal_Payable") as "outstandingloan", T0."User_ID", T0."Due_Date" from public.emi_schedule as T0, public.order_details as T1
where
T0."EMI_Amount" is not null and
T0."Loan_Status" != 'cancelled' and
(T0."Payment_Status" = 'pending' or (T0."Payment_Status" = 'paid' and T0."Paid_Date" > '2017-01-01')) and
T0."Order_ID" = T1."order_id" and
T1."order_status" != 'refunded' and
T1."order_status" != 'refundReceived' and
T0."Due_Date" < current_date
  
  ) as T3
group by T3."User_ID",T3."Due_Date"
)
  select dpd_range,  count from(
select '0-30' as dpd_range,  count(users) from T4 where "DPD" = '2017-01-05' and ("outstandingloan1" between 7001 and 15000)
group by dpd_range
UNION
select '30-60' as dpd_range, count(users) from T4 where "DPD" = '2016-12-05' and ("outstandingloan1" between 7001 and 15000)
group by dpd_range
UNION
select '60+' as dpd_range, count(users) from T4 where "DPD" <= '2016-11-05' and ("outstandingloan1" between 7001 and 15000)
group by dpd_range

order by dpd_range) A),
T9 as
(
  with T4 as
(
select (min(T3."Due_Date")) as "DPD", T3."User_ID" as users, T3."Due_Date", (sum(T3."outstandingloan")) as "outstandingloan1" from
(
select (T0."Outstanding_Balance" + T0."Principal_Payable") as "outstandingloan", T0."User_ID", T0."Due_Date" from public.emi_schedule as T0, public.order_details as T1
where
T0."EMI_Amount" is not null and
T0."Loan_Status" != 'cancelled' and
(T0."Payment_Status" = 'pending' or (T0."Payment_Status" = 'paid' and T0."Paid_Date" > '2017-01-01')) and
T0."Order_ID" = T1."order_id" and
T1."order_status" != 'refunded' and
T1."order_status" != 'refundReceived' and
T0."Due_Date" < current_date
  
  ) as T3
group by T3."User_ID",T3."Due_Date"
)
  select dpd_range,  count from(
select '0-30' as dpd_range,  count(users) from T4 where "DPD" = '2017-01-05' and ("outstandingloan1" between 15001 and 30000)
group by dpd_range
UNION
select '30-60' as dpd_range, count(users) from T4 where "DPD" = '2016-12-05' and ("outstandingloan1" between 15001 and 30000)
group by dpd_range
UNION
select '60+' as dpd_range, count(users) from T4 where "DPD" <= '2016-11-05' and ("outstandingloan1" between 15001 and 30000)
group by dpd_range

order by dpd_range) A),
T10 as 
(
  with T4 as
(
select (min(T3."Due_Date")) as "DPD", T3."User_ID" as users, T3."Due_Date", (sum(T3."outstandingloan")) as "outstandingloan1" from
(
select (T0."Outstanding_Balance" + T0."Principal_Payable") as "outstandingloan", T0."User_ID", T0."Due_Date" from public.emi_schedule as T0, public.order_details as T1
where
T0."EMI_Amount" is not null and
T0."Loan_Status" != 'cancelled' and
(T0."Payment_Status" = 'pending' or (T0."Payment_Status" = 'paid' and T0."Paid_Date" > '2017-01-01')) and
T0."Order_ID" = T1."order_id" and
T1."order_status" != 'refunded' and
T1."order_status" != 'refundReceived' and
T0."Due_Date" < current_date
  
  ) as T3
group by T3."User_ID",T3."Due_Date"
)
  select dpd_range,  count from(
select '0-30' as dpd_range,  count(users) from T4 where "DPD" = '2017-01-05' and "outstandingloan1" > 30000
group by dpd_range
UNION
select '30-60' as dpd_range, count(users) from T4 where "DPD" = '2016-12-05' and "outstandingloan1" > 30000
group by dpd_range
UNION
select '60+' as dpd_range, count(users) from T4 where "DPD" <= '2016-11-05' and "outstandingloan1" > 30000
group by dpd_range

order by dpd_range) A)

select T6.dpd_range,(T6.count) as "OS(<1K)", (T7.count) as "OS(1001-7000)", (T8.count) as "OS(7001-15000)", (T9.count) as "OS(15001-30000)", (T10.count) as "OS(>30K)", (T5.sum) as "TOTAL OS" from T6
FULL OUTER JOIN T7 on
T7.dpd_range = T6.dpd_range
FULL OUTER JOIN T8 on
T8.dpd_range = T6.dpd_range
FULL OUTER JOIN T9 on
T9.dpd_range = T6.dpd_range
FULL OUTER JOIN T10 on
T10.dpd_range = T6.dpd_range
FULL OUTER JOIN T5 on
T5.dpd_range = T6.dpd_range
