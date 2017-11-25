## Text
Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.

## Solution
```javascript
function attendEveryMeeting(meetings) {
  let attendEverything = true;
  meetings.sort((a, b) => a[0] - b[0]);
  for(let i=1; i<meetings.length; i++) {
    attendEverything = attendEverything && meetings[i][0] > meetings[i-1][1];
  }
  return attendEverything;
}
```

## Explaining

## Testcase
- attendEveryMeeting([[0, 30],[5, 10],[15, 20]]) = false
- attendEveryMeeting([[5, 10],[15, 20], [0, 30]]) = false
- attendEveryMeeting([[5, 10],[15, 20]]) = true
- attendEveryMeeting([[15, 20], [5, 10]]) = true

## Complexity
O(nlogn + n)
