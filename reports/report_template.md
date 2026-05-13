# Báo Cáo Reliability Ngày 10

**Ho Va Ten:** Thái Tuấn Khang 2A202600289

## 1. Tổng quan kiến trúc

Mô tả gateway, circuit breaker, fallback chain và các tầng cache.
Bao gồm một sơ đồ đơn giản (text/ASCII được chấp nhận):

```
User Request
    |
    v
[Gateway] ---> [Kiểm tra Cache] ---> HIT? trả về cached
    |                                 |
    v                                 v MISS
[Circuit Breaker: Primary] -------> Provider A
    |  (OPEN? bỏ qua)
    v
[Circuit Breaker: Backup] --------> Provider B
    |  (OPEN? bỏ qua)
    v
[Thông báo fallback tĩnh]
```

## 2. Cấu hình

| Setting | Value | Reason |
|---|---:|---|
| failure_threshold | TODO | TODO |
| reset_timeout_seconds | TODO | TODO |
| success_threshold | TODO | TODO |
| cache TTL | TODO | TODO |
| similarity_threshold | TODO | TODO |
| load_test requests | TODO | TODO |

## 3. Định nghĩa SLO

Định nghĩa các SLO mục tiêu và liệu hệ thống của bạn có đạt được hay không:

| SLI | SLO target | Actual value | Met? |
|---|---|---:|---|
| Availability | >= 99% | TODO | TODO |
| Latency P95 | < 2500 ms | TODO | TODO |
| Fallback success rate | >= 95% | TODO | TODO |
| Cache hit rate | >= 10% | TODO | TODO |
| Recovery time | < 5000 ms | TODO | TODO |

## 4. Metrics

Dán hoặc tóm tắt `reports/metrics.json`.

| Metric | Value |
|---|---:|
| availability | TODO |
| error_rate | TODO |
| latency_p50_ms | TODO |
| latency_p95_ms | TODO |
| latency_p99_ms | TODO |
| fallback_success_rate | TODO |
| cache_hit_rate | TODO |
| estimated_cost_saved | TODO |
| circuit_open_count | TODO |
| recovery_time_ms | TODO |

## 5. So sánh Cache

Chạy simulation với cache bật và tắt. Điền vào cả hai cột:

| Metric | Without cache | With cache | Delta |
|---|---:|---:|---|
| latency_p50_ms | TODO | TODO | TODO |
| latency_p95_ms | TODO | TODO | TODO |
| estimated_cost | TODO | TODO | TODO |
| cache_hit_rate | 0 | TODO | TODO |

## 6. Redis shared cache

Giải thích tại sao shared cache quan trọng cho production:

- Tại sao in-memory cache không đủ cho multi-instance deployments: TODO
- Cách `SharedRedisCache` giải quyết vấn đề này: TODO

### Bằng chứng của shared state

Cho thấy hai cache instance riêng biệt có thể thấy cùng một dữ liệu:

```
# Paste test output hoặc script output thể hiện shared state
TODO
```

### Redis CLI output

```bash
# docker compose exec redis redis-cli KEYS "rl:cache:*"
TODO
```

### So sánh latency In-memory vs Redis (tùy chọn)

| Metric | In-memory cache | Redis cache | Notes |
|---|---:|---:|---|
| latency_p50_ms | TODO | TODO | |
| latency_p95_ms | TODO | TODO | |

## 7. Các kịch bản Chaos

| Scenario | Expected behavior | Observed behavior | Pass/Fail |
|---|---|---|---|
| primary_timeout_100 | Tất cả traffic fallback sang backup, circuit mở | TODO | TODO |
| primary_flaky_50 | Circuit dao động, mix primary và fallback | TODO | TODO |
| all_healthy | Tất cả request qua primary, không circuit mở | TODO | TODO |
| (kịch bản của bạn) | TODO | TODO | TODO |

## 8. Phân tích lỗi

Giải thích một điểm yếu còn lại và cách bạn sẽ sửa nó trước khi production:

- Điều gì có thể sai?
- Bạn sẽ thay đổi gì? (ví dụ: Redis circuit state, per-user rate limiting, quality SLO)

## 9. Các bước tiếp theo

Liệt kê 2-3 cải tiến cụ thể bạn sẽ thực hiện:

1. TODO
2. TODO
3. TODO

---

