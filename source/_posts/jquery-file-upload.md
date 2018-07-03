---
title: jquery file upload
date: 2018-07-03 11:41:40
tags: [jquery, java]
categories: 前端
description: 'jquery文件上传demo'
---

## 单控件文件上传DEMO 

 js根据ID java根据name


	<input type="file" name="editMyimg" id="editMyimg">

	js:

	$.ajaxFileUpload({
		url: '${home}/party/admin/article.json',
		dataType: 'json',
		secureuri: false,
		data: {
		action: "updateData",
		title: title,
		briefInfo: briefInfo,
		id: id
		},
		fileElementId: 'editMyimg',
		success: function () {
		backcall()
		    }
	});

	java (springMVC) :

	@RequestMapping
	public ActionResult updateData(PartyArticleQuery partyArticleQuery, @RequestParam("editMyimg") MultipartFile file) {
	    ActionResult actionResult = ActionResult.ok();
	
	    String img = "";
	if (!file.isEmpty()) {
	if (!StrUtils.empty(file.getOriginalFilename())) {
	            File toFile = null;
	try {
	                                   toFile = PathUtils.getUpload(PathUtils.PATH_PARTY_ARTICLE, file.getOriginalFilename(), StrUtils.getUUID());
	                file.transferTo(toFile);
	            } catch (IOException e) {
	                PathUtils.delFile(toFile);
	return ActionResult.error("图片上传失败");
	            }
	            img = PathUtils.getUploadPath(toFile);
	            partyArticleQuery.setImg(img);
	        }
	    }
	    Integer integer = partyArticleService.updateData(partyArticleQuery);
	return actionResult;
	}