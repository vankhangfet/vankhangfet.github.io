---
layout: post
title: Unit Test - What are diffrences between @Mocked and @Injectable in JMockit
tags: [Unit Test]
---


Dự án trước chúng tôi có cơ hội làm việc với thư viện Jmockit để thực hiện viết Unit test. Về cảm nhận thì Jmockit khá đơn giản, dễ dùng.

Tuy nhiên có một số concept và từ khóa đôi khi gây khó hiểu đó là @Mocked và @Injectable. 

Trong mọi trường hợp thì @Mocked sẽ mock cho tất cả các instance của class đó, còn @Injectable sẽ chỉ mock cho cụ thể method / field. 

Theo kinh nghiệm thì chúng ta có thể tóm tắt @Mocked và @Injectable như dưới đây:

- @Injectable sẽ được dùng khi bạn có thể PASS instance mà mark @Injectable vào trong class bạn muốn test 

- @Mocked được dùng khi bạn không thể PASS instance mà mark @Mocked vào trong class bạn muốn test. 

Chúng ta xem xét ví dụ sau. Chúng ta có một class đó là "Team"
~~~~
public class Team {
    public Team(Leader leader) {
        //...
    }
    
    public boolean hasADiscussion() {
        System.out.println(leader.getName());
        Discussion d = new Discussion();
        return d.started();
    }
}
~~~~

Ở class này, chúng ta có thể inject/pass một instance Leader vào trong constructer của "Team". Tuy nhiên với function hasADiscussion() thì chúng ta không thể truyền 
intance Discussion vào được. Như vậy chúng ta có thể phải dùng cả @Injectable và @Mocked.

~~~~
public class TeamTests {

    @Injectable Leader aLeader;
    /**
		* Usually you will write `@Mocked Leader aLeader`, which is fine in most 
		* cases but you will hit hidden issues when mocking too much than what you need
		*/
    @Mocked Discussion aDiscussion;
    
    @Test
    public void testHasADiscussion() {
        new NonStrictExpectations() {{
            aLeader.getName(); result = "dev_leader";
            aDiscussion.start(); result = true;
        }};
        
        Team t = new Team(aLeader); // Note! You can pass in `aLeader` (but not aDiscussion) to `Team` here!
        assertTrue(t.hasADiscussion());
    }
}
~~~~

Refer: https://bowenli86.github.io/2016/04/06/test/jmockit/Unit-Test-JMockit-What-are-the-differences-between-Mocked-and-Injectable-in-JMockit-and-when-to-use-Injectable-rather-than-Mocked/



