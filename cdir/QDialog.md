## QDialog

* show 和 exec 

  ```c++
  ///>下面这两种方式会有不同的效果，通过new 申请的可以一直存在，dlg会在作用域到了后自动释放
  QDialog * dlg = new QDialog;
  dlg->show();
  
  QDialog dlg;
  dlg.show();
  setModel 也可以设置模态
  exec 函数运行会阻塞，而show函数运行完后可以继续执行后续的内容。通过exec执行的对话框会返回一个值，表示当前对话框的状态。
  accept();//可以将模态对话框隐藏，
  ```

## QColorDialog

```c++
QColor color = QColorDialog::getColor(Qt::red,this,tr("颜色对话框"));
QColor(alpha,1,0,0)//第一个参数表示透明度，为1表示完全不透明，后3个数表示颜色，越大表示颜色越深，可以用0-1或0-255，进行相应的数学转换就行。
```



## QInputDialog

```
QInputDialog::getText,
QInputDialog::getItem,
QInputDialog::getInt,
//可以获取需要的变量值
```

## QMessageBox

```
warning ,
information,
critical,
question
```

