define(function(require, exports, module) {
			var tpl = require('text!publicVueComponent/emapflowview/emapflowview.html?v=20201028');
			return function() {
				var page = {
					template : tpl,
					props : ['taskid', 'processid', 'hideUserId'],
					data : function() {
						return {
							items : []
						};
					},
					mounted : function() {
						var that = this;
						var urlParam = 'taskId=' + this.taskid;
						if (this.processid != null && this.processid != "") {
							urlParam = 'processInstanceId=' + this.processid;
						}
						MOB_UTIL.Post(WIS_CONFIG.ROOT_PATH
								+ "/sys/emapflow/tasks/queryFlowState.do?"
								+ urlParam + "&responseType=JSON").then(
								function(response) {
									// console.log(response)
									var data = response;
									for (var i = 0; i < data.length; i++) {
			                            var assignee = data[i].assignee;
										if(that.hideUserId==true){
											assignee = assignee.replace(/\((([^()]*|\([^()]*\))*)\)/g,'');
										}
										data[i].assignee = assignee;
										// type重新赋值
										if (data[i].flowComment == "取回") {
											data[i].type = "撤回";
											data[i].flowComment = '';
										} else if (data[i].typeCode == "turnback") {
											data[i].type = "退回";
										} else if (data[i].typeCode == "completed"
												&& data[i].nodeId == "usertask1") {
											data[i].type = "提交";
											data[i].flowComment = '';
										} else if (data[i].typeCode == "completed"
												&& data[i].nodeId != "usertask1") {
											data[i].type = "通过";
										}
									}
									that.items = data;
								});
					},
					methods : {
						getStatus : function(item) {
							if (item.typeCode == "turnback"
									|| item.typeCode == "termination") {
								return "error";
							} else {
								return item.typeCode == null
										? "process"
										: "finish";
							}
						}
					}
				};
				return page;
			};
		});