# Repayment Split Calculator

一个单文件 HTML 还款计算器，用来把一笔还款拆分成“本金”和“利息”。

## 这个页面是干嘛的

页面支持输入：

- 借款总额
- 年利率
- 本次还款金额
- 还款日期

页面会输出：

- 本次归还本金
- 本次支付利息
- 还款后剩余本金
- 还款日期距离 `2026-01-01` 的天数

## 计算逻辑

这个计算器把 `2026-01-01` 作为基准日。

设：

- `daysElapsed` = 还款日期距离 `2026-01-01` 的天数
- `annualRate` = 年利率对应的小数值，例如 `10% = 0.10`
- `paymentAmount` = 本次还款金额
- `principalRepaid` = 本次还款中实际归还的本金

使用公式：

```text
(1 + daysElapsed / 365 * annualRate) * principalRepaid = paymentAmount
```

推导后可得：

```text
principalRepaid = paymentAmount / (1 + daysElapsed / 365 * annualRate)
interestPaid = paymentAmount - principalRepaid
remainingPrincipal = originalPrincipal - principalRepaid
```

例如：

- 如果还款日期是 `2026-01-02`，那么 `daysElapsed = 1`
- 如果年利率输入 `10`，页面会按 `0.10` 参与计算

## 本地打开

直接用浏览器打开 `index.html` 即可。

## GitHub Pages

仓库内置了 GitHub Actions workflow。

当代码推送到 `main` 分支后，workflow 会自动把静态页面发布到 GitHub Pages。
