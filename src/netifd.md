>##NETIFD learn##
>
>>日志记录函数：
>>`netifd_log_message(L_NOTICE, "%s '%n' dev_name is %s\n", __FUNCTION__, __LINE__, dev_name );`

---
>>```ubus call network reload```->
>>|
>>|---->`netifd_handle_reload()`->`netifd_reload()`->
>>|---->`config_init_all()`->`config_init_wireless()`->
>>|---->`wireless_device_create()`->`wireless_device_script_task_cb()`
>>|---->`wireless_device_mark_down()`->
>>|---->`wireless_device_retry_setup()`->
>>>|---->`wireless_interface_handle_link()`->
>>>|---->`interface_handle_link()`
