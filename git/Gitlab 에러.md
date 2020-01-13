# Gitlab 관련 에러사항

1. Processing by MetricsController#index as HTML 에러
아직 미해결
```
Found and solved the problem. In the nginx configuration in my gitlab.rb I used a depricated setting which was removed in version 11.
old:
nginx['listen_address'] = 'MY_IP_ADDRESS'
changed to:
nginx['listen_addresses'] = ["MY_IP_ADDRESS"]
```