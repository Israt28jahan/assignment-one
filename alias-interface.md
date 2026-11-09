Type Alias VS Interface
TypeScript নিয়ে কাজ করতে গিয়ে আমরা একটা সমস্যার সম্মুখীন প্রতিনিয়ত হই , সেটা হল কি টাইপের ডেটা হবে তা বর্ননা করতে গিয়ে বুঝতে পারি না যে কখন আসলে Type alias ব্যবহার করব আর কখন Interface কারন এই দুটি জিনিস দেখতে প্রায়ই একই রকম ।
 নিচে কিছু মিল এবং অমিল বর্ননা করা হলো যাতে সহজেই আমরা চিনতে পারি ঃ

 মিলঃ
 Type "Alias" মানে হলো আমরা নিজের পছন্দসই একটা নাম দিতে পারি আর Interface এর মাধ্যমে আমরা সাধারনত একটি Object কে বর্ননা করে থাকি . আশা করি নিচে একটি উদাহরন দিলে বুঝতে পারবে ঃ

 type TUser = {
  id: number;
  name: string;
};

interface IUser {
  id: number;
  name: string;
}

const user1: TUser = { id: 1, name: "Mir" };
const user2: IUser = { id: 2, name: "Mizan" };

 অমিলঃ
Interface সাধারনত একটি মডেলের নকশার মতো কাজ করে । একটি থেকে আরেকটি নকশা বানাতে গেলে Interface এ Extends শব্দটি ব্যবহার করতে হয় আর একই কাজ Type alias এ করতে গেলে & ব্যবহার করতে হ
হয়.

interface IPerson {
  name: string;
}
interface IEmployee extends IPerson {
  salary: number;
}

type TPerson = {
  name: string;
};
type TEmployee = TPerson & {
  salary: number;
};
 আরও একটি উল্লেখযোগ্য পার্থক্য হচ্ছে একই নামের প্রপার্টির টাইপ না মিললে দুটোর আচরণ করে .
 interface A {
  id: number;
}
interface B extends A {
  id: string; 
}

type C = { id: number };
type D = C & { id: string }; 
const d: D = { id: "abc" };

একই নামে দুইবার `interface` লিখলে TypeScript দুটোকে মিলিয়ে একটা বানিয়ে দেয়। একে বলে declaration merging। `type`-এর ক্ষেত্রে তা হয় না, ভুল আসে:

ts
interface IStudent {
  name: string;
}
interface IStudent {
  age: number;
}
 এখন IStudent = { name: string; age: number }
const student: IStudent = { name: "Mir", age: 22 };

type TStudent = { name: string };
type TStudent = { age: number }; 

এইবার আসা যাক কখন কোনটা ব্যবহার করবঃ
Interface:
১  Object এর আকার বর্ননা করতে
২  API থেকে কোনো মডেল আসলে
Type Alias:
১ যেখানে Union দরকার . Reject | approved
২ কয়েকটি টাইপ মিলিয়ে জটিল একটি টাইপ বানাতে হলে

পরিশেষে বলা যায় বাস্তব প্রজেক্টে `type` আর `interface` একে অপরের বিপরীত নয়, বরং একে অপরের বন্ধু


