[[Shema Serializer]]

# [Thans Schema Serializer Example](https://codesandbox.io/s/gp-serializer-bn790v?file=/src/serializer/workday/submit-customer.serializer.ts)

## Tags:
#job

## Questions:
- Is ![[Screenshot 2022-03-28 at 10.32.26.png]] instance of this class object with "wd:Sbumit_Customer_Request"  as property
	- **yes**
- Why use `@Exclude` for private properties of classes
	- **b/c xml2js converted the private properties as well as the public ones**
- Why use any in ![[Screenshot 2022-03-28 at 10.40.36.png]] and not some stricter type
	- **to keep the classes generic for now, in the future types could be replaced with the correct types**
- Why not use HeaderSecurity type instead of any ![[Screenshot 2022-03-28 at 10.42.51.png]]
- Explain this type ![[Screenshot 2022-03-28 at 10.45.19.png]]
	- **a new class of any type**
- Do we put serializers into serializers folder and not each serializer into corresponding folder

## Conclusions
![[Screenshot 2022-03-28 at 10.49.56.png]]
Test:
- Type
- Structure
- Inputed value
- Is strictly equal test needed ?