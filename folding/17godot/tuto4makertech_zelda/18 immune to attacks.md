## 230927

## 0035 intro

## 0152 修改代码，产生免疫，但第一次免疫后就再也不会被攻击。

## 0247 加一行代码，就可以让闪烁结束后就能再被攻击。调整 hurttimer 时间就可以控制免疫时间。

## 由于之前的判定是\_on_hurt_box_area_entered，所以当玩家免疫时间已经过了，但玩家和怪物碰撞模型仍然重叠时（即没有新的 area entered），玩家就不再会被伤害。这里就修复这个 bug
