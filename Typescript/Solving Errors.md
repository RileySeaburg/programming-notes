# Solving Typescript Errors

As your writing your typescript #code you may come across some #errors that scare you. Do not be deterred typescript is just telling you there may be an issue with your code. #Typescript is only as smart as the code you give it. Thus it may require additional context (and time) to write bug free typescript code but in the end it is worth it and often even quicker. 

#Example:
You're calling data from an API and using [GraphQL CodeGen](https://www.graphql-code-generator.com/) to generate types for the data is coming through. 

#GraphqlCodeGen wants to leave space for the possibility that the data is undefined so your type may look something like this. 

#### Generated TypeScript Type Example

```
/\*\* Field Group \*/

export type Page\_Revenuesection = AcfFieldGroup & {

 \_\_typename?: 'Page\_Revenuesection';

 /\*\* The bullet points go here \*/

 bulletPoints?: Maybe<Array<Maybe<Page\_Revenuesection\_BulletPoints\>>>;

 /\*\* The name of the ACF Field Group \*/

 fieldGroupName?: Maybe<Scalars\['String'\]>;

 /\*\* The image that appears on the left side of the section. \*/

 sectionImage?: Maybe<MediaItem\>;

 /\*\*

 \* The text in the section.

 \* Contains a headline that is partially highlighted,

 \* a sub headline and a list of three items.

 \*/

 sectionText?: Maybe<Page\_Revenuesection\_SectionText\>;

};
```



In the above example you can see the "maybe" word used multiple times. This is how Graphql Code generator leaves room for data to be undefined.

### Solving The 'Undefined' and the "Maybe' Problem

This assertion is not definite however and this typescript will often warn you when you are trying to work with the actual object the type is referring to. 

To overcome this lack of certainty Typescript offers an assertion operator available as "!" see the example below.

#### Typescript Assertion Example
```
 const headlineText: sectionHeadlineType = sectionHeadline!;
```

As you can see this #operator gets attached to the end of an #object when chaining or #destructing to inform Typescript that "you know what you're doing" and that you know the #data will be available as that #type.

This #assertion solves the non existing #error and the see below:

#### Typescript Error Examples
##### #ts2339
```
Property 'sectionHeadline' does not exist on type 'Maybe<Page\_Revenuesection\_SectionText> | undefined'.ts(2339)
```

##### #ts2322
```
Type 'Maybe<Page\_Revenuesection\_SectionText\_SectionHeadline> | undefined' is not assignable to type 'Page\_Revenuesection\_SectionText\_SectionHeadline'.  
Type 'undefined' is not assignable to type 'Page\_Revenuesection\_SectionText\_SectionHeadline'.  
Type 'undefined' is not assignable to type 'AcfFieldGroup'.ts(2322)
```