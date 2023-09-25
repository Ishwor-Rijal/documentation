# `Simple Query Language `
###### `*` If you want to work on a block of query statements like deleting a bulk organisations and their associated data in foreign tables, following queries might be helpful ...
***
## Select Apprenticeships
###### If you have `apprenticeships` table where `organisation_id` is represented by `employer_id` and you have to remove associated data of organisation_ids `2`, `6`, `7` :
you can first observe the aassociated apprenticeships as :
#
```sh
SET @ids = '7,6,2';
SELECT * FROM apprenticeships WHERE FIND_IN_SET(employer_id, @ids);
```

## Delete Apprenticeships

```sh
SET @ids = '7,6,2';
DELETE FROM apprenticeships WHERE FIND_IN_SET(employer_id, @ids);
```
#
#
#
***
###### If you have `occupations` table with `organisation_id` and you have to remove associated data of organisations with id `2`, `6`, `7` :
you can first observe the aassociated occupations as :
#
## Select Occupation

```sh
SET @ids = '7,6,2';
SELECT * FROM occupations WHERE FIND_IN_SET(organisation_id, @ids);
```

## Delete Occupations

```sh
SET @ids = '7,6,2';
DELETE FROM occupations WHERE FIND_IN_SET(organisation_id, @ids);
```
#
#
#
***
###### If you have `users` table which is associated to `members.user_id` of `members` table  and member belongs to `organisation`. i.e. if you have to remove users associated to members belonging to organisations with id `2`, `6`, `7` :
you can first observe the aassociated users as :
#
## Select Users

```sh
SET @ids = '7,6,2';
SELECT * FROM users where users.id in (select user_id from members WHERE FIND_IN_SET(organisation_id, @ids));
```
## See Associated User and Member Details 

```sh
SET @ids = '7,6,2';
SELECT members.first_name, members.last_name, members.organisation_id, users.id as uid from users inner join members on users.id=members.user_id WHERE FIND_IN_SET(organisation_id,@ids));
```

## Delete Users

```sh
SET @ids = '7,6,2';
DELETE FROM users where users.id in (select user_id from members WHERE FIND_IN_SET(organisation_id, @ids));
```

#
#
#
***
###### If you have `enrolments` table which is associated to `members` table ( i.e `enrolments.member_id` = `members.id` )  and member belongs to `organisation`. i.e. if you have to remove enrolments of members belonging to organisations with id `2`, `6`, `7` :
you can first observe the aassociated enrolments as :
#

## Select Enrolments

```sh
SET @ids = '7,6,2';
SELECT FROM enrolments where enrolments.member_id in (select id from members WHERE FIND_IN_SET(organisation_id, @ids));
```
## See Enrolment Details 

```sh
SET @ids = '7,6,2';
SELECT members.first_name, members.last_name, members.organisation_id, enrolments.id as enrolment_id, enrolments.course_id as course_id from enrolments inner join members on members.id=enrolments.member_id WHERE FIND_IN_SET(organisation_id,@ids);
```

## Delete Enrolments

```sh
SET @ids = '7,6,2';
DELETE FROM enrolments where enrolments.member_id in (select id from members WHERE FIND_IN_SET(organisation_id, @ids));
```

#
#
#
***
###### If you have `members` table with `organisation_id` and you need to remove `members` belonging to organisations with id `2`, `6`, `7` :
you can first observe the aassociated members as :
#
## Select Members

```sh
SET @ids = '7,6,2';
SELECT *  FROM members WHERE FIND_IN_SET(organisation_id, @ids);
```

## Delete Members

```sh
SET @ids = '7,6,2';
DELETE FROM members WHERE FIND_IN_SET(organisation_id, @ids);
```

#
#
#
***
###### If you have to remove simply `organisations` with id `2`, `6`, `7` :
you can first observe the aassociated organisations as :
#
## Select Orgainsations

```sh
SET @ids = '7,6,2';
SELECT * FROM organisations WHERE FIND_IN_SET(id, @ids);
```

## Delete Organisations

```sh
SET @ids = '7,6,2';
DELETE FROM organisations WHERE FIND_IN_SET(id, @ids);
```
