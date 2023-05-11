```
("select user.id as userid, " +
        "group_concat(concat_ws(',',order_detail.name,totalnumber,order_detail.amount) separator ';') as jsonstr " +
        "from user " +
        "inner join (  select user.id as userid, order_detail.name, sum(order_detail.number) as totalnumber,order_detail.amount " +
        "               from user " +
        "               inner join user_order on user.id = user_order.user_id " +
        "               inner join order_detail on user_order.id = order_detail.order_id " +
        "               group by user.id, order_detail.name,order_detail.amount" +
        "            ) as order_detail on order_detail.userid = user.id " +
        "group by user.id")