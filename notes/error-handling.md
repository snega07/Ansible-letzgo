Execution of task flow->

lood
when cond
register
ansible_facts
set_fact
var in task

If there are 3 task. 

Ansible will execute Task 1 first only if it is completed and success. It will move to next task.
Also this failure is host specific. Failure in one host does not affect other.
ignore errors: ignore all
failed_when:
result.rc==0
"no such" in result.stdout

block 
rescue

Task:

Check if openssl/openssh exits. Ignore if error
check Docker exists. Ignore if error. Store the state of presence in variable using register and use that output in next step
Use when condition and install docker if it does not exists. use output.failed
