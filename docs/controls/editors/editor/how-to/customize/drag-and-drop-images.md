---
title: Drag and Drop Images
page_title: Drag and Drop Images | Kendo UI Editor
description: "Learn how drag and drop images in the Kendo UI Editor widget."
previous_url: /controls/editors/editor/how-to/drag-and-drop-images
slug: howto_drag_and_drop_images_editor
---

# Drag and Drop Images

The following example demonstrates how to drag and drop images in the Kendo UI Editor.

As an image source, the demo uses a TreeView. However, you can use any custom HTML markup in combination with the [Kendo UI Drag and Drop framework](http://demos.telerik.com/kendo-ui/web/dragdrop/index.html).

```dojo
  <style>

    html
    {
      font: 12px sans-serif;
    }

    html,
    body
    {
      height: 100%;
      padding: 0;
      margin: 0;
    }

    #treeview,
    #editorWrapper
    {
      float: left;
    }

    #treeview
    {
      width: 200px;
    }

    #editorWrapper
    {
      width: 600px;
      position: relative;
    }

    #editorWrapper .k-loading-image
    {
      display: none;
    }

  </style>
  <div>

    <div id="treeview"></div>

    <div id="editorWrapper">
      <textarea id="editor" cols="30" rows="10"></textarea>
    </div>

  </div>
  <script>

    $(function(){

      var body = $(document.body);

      var editorWrapper = $("#editorWrapper");

      function onDragStart(e) {
        if (!e.sender.dataItem(e.sourceNode).value) {
          e.preventDefault();
        } else {
          kendo.ui.progress(editorWrapper, true);
        }
      }

      function onDrag(e) {
        if ($(e.dropTarget).closest(editorWrapper)[0]) {
          e.setStatusClass("k-add");
        } else {
          e.setStatusClass("k-denied");
        }
      }

      function onDrop(e) {
        if ($(e.dropTarget).closest(editorWrapper)[0]) {
          e.preventDefault();
          var img = '<img src="' + e.sender.dataItem(e.sourceNode).value + '" alt="image" />';
          $("#editor").data("kendoEditor").exec("inserthtml", {value: img});
        }
        kendo.ui.progress(editorWrapper, false);
      }

      $("#treeview").kendoTreeView({
        dataSource: {
          data: [
            {text: "Images", value: null, expanded: true, items: [
              {text: "Telerik logo", value: "http://www.telerik.com/sfimages/default-source/logos/telerik-logo-reversed.png", spriteCssClass: "k-icon k-i-plus"},
              {text: "Kendo UI Dojo logo", value: "http://trykendoui.telerik.com/images/logo.png", spriteCssClass: "k-icon k-i-plus"}
            ]}
          ]
        },
        dataTextField: "text",
        dataValueField: "value",
        dragAndDrop: true,
        dragstart: onDragStart,
        drag: onDrag,
        drop: onDrop
      });

        $("#editor").kendoEditor({
        tools: [
          "insertImage"
        ]
      });     

    });

  </script>
```

## See Also

* [Basic Usage of the Editor (Demo)](https://demos.telerik.com/kendo-ui/editor/index)
* [Using the API of the Editor (Demo)](https://demos.telerik.com/kendo-ui/editor/api)
* [JavaScript API Reference of the Editor](/api/javascript/ui/editor)
