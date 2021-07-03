# Common LispでRSAを実装してみる。

Common Lispにはprime?などという関数はなさそうなのでまずはそれから自作するところからはじめる。

```
(defun mirror-rabin-test (value)
  (let ((v value))
	(loop for i from 5 to (1- value) by 6
	   until (or (null v) (> i value))
	   do
		 (when (or (zerop (mod value i)) (zerop (mod value (+ i 2))))
			(setf v nil)))
	v))
```
