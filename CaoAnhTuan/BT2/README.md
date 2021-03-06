#Bài tập tuần 5

##Mô tả bài toán
* Kiểm tra số được nhập có phải số điện thoại hay không
* Các điều kiện:
	* Kí tự đầu tiên phải là số ‘0’.
	* Độ dài chuỗi kí tự phải là 10 hoặc 11.
	* Kí tự trong chuỗi phải là một số.

##Lớp cần kiểm thử
```java
	public class SoDienThoai {
		public static String s1 = "La mot so dien thoai hop le";
    		public static String s2 = "Khong phai la mot so dien thoai hop le";

    		public String ktraSDT(String s3) {
        		boolean dk1 = (s3.charAt(0)=='0');
        		boolean dk2 = (s3.length()==10 || s3.length()==11);

        		int i=1;
        		if (dk1 && dk2){
            			while (i < s3.length()) {
                			if (s3.charAt(i)>=48 && s3.charAt(i)<=57);else {
                    				break;
                			}
                			if (i + 1 == s3.length()) {
                    				return s1;
                			}i++;
            			}
        		}return s2;
    		}
	}
```
##Áp dụng tiêu chuẩn MCDC
Tóm tắt:
```
if (C1 && C2){
	while (C3){
		if(C4 && C5)
		if(C6)
	}
}
```
* Xét điều kiện 1 và 2:

\#       |    C1    |    C2    |    C3
-------|------------|------------|---------------------------|
1.       |F                |F                | T
2.       |F                |T                | F
3.       |T                |F                | F
4.       |T                |T                | T

* Xét điều kiên 1,2 và 3:

\#       |   C12    |    C3    |    C123
-------|------------|------------|---------------------------|
1.       |T                |F                | F
2.       |F                |F                | T
3.       |F                |T                | F
4.       |T                |T                | T

* Xét điều kiện 4 và 5:

\#       |    C4    |    C5    |    C45
-------|------------|------------|---------------------------|
1.       |F                |F                | T
2.       |F                |T                | F
3.       |T                |F                | F
4.       |T                |T                | T
* Xét điều kiện 1,2,3,4 và 5:

\#       |   C123   |    C45   |   C12345
-------|------------|------------|---------------------------|
1.       |F                |F                | T
2.       |F                |T                | F
3.       |T                |F                | F
4.       |T                |T                | T
	
* Xét điều kiện 1,2,3 và 6:

\#       |   C123   |    C6    |   C1236
-------|------------|------------|---------------------------|
1.       |F                |F                | T
2.       |F                |T                | F
3.       |T                |F                | F
4.       |T                |T                | T

Từ bảng trên ta xây dựng được các test cases:

##Unit Test cho các ca kiểm thử
```java
        @Test
	public void test0() {
		SoDienThoai soDienThoai = new SoDienThoai();
		Assert.assertEquals(soDienThoai.ktraSDT("999459090"), soDienThoai.s2);
	}

	@Test
	public void test1() {
		SoDienThoai soDienThoai = new SoDienThoai();
		Assert.assertEquals(soDienThoai.ktraSDT("0164747145"), soDienThoai.s2);
	}
	
	@Test
	public void test2() {
		SoDienThoai soDienThoai = new SoDienThoai();
		Assert.assertEquals(soDienThoai.ktraSDT("01647471457"), soDienThoai.s2);
	}
	
	@Test
	public void test3() {
		SoDienThoai soDienThoai = new SoDienThoai();
		Assert.assertEquals(soDienThoai.ktraSDT("012345696"), soDienThoai.s2);
	}
	
	@Test
	public void test4() {
		SoDienThoai soDienThoai = new SoDienThoai();
		Assert.assertEquals(soDienThoai.ktraSDT("013234567896"), soDienThoai.s2);
	}
	
	@Test
	public void test5() {
		SoDienThoai soDienThoai = new SoDienThoai();
		Assert.assertEquals(soDienThoai.ktraSDT("0164747145a"), soDienThoai.s2);
	}
	
	@Test
	public void test6() {
		SoDienThoai soDienThoai = new SoDienThoai();
		Assert.assertEquals(soDienThoai.ktraSDT("0123456%235"), soDienThoai.s2);
	}
```
##Đo mức độ bao phủ: