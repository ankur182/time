So I have made a asset object of aircraft and we basically check that facilitybnppshare data is same as savebnppshare data and also the as we want to verify that the changes in bnppshare for that particular facility is aligned to that asset also, is there any improvement required in the code to run this test function




/*C++ program to read time in HH:MM:SS format and convert into total seconds.*/
 
#include <iostream>
#include <iomanip>
 
using namespace std;
class Time
{
    private:
        int seconds;
        int hh,mm,ss;
    public:
        void getTime(void);
        void convertIntoSeconds(void);
        void displayTime(void);
};
 
void Time::getTime(void)
{
    cout << "Enter time:" << endl;
    cout << "Hours?   ";          cin >> hh;
    cout << "Minutes? ";          cin >> mm;
    cout << "Seconds? ";          cin >> ss;
}
 
void Time::convertIntoSeconds(void)
{
    seconds = hh*3600 + mm*60 + ss;
}
 
void Time::displayTime(void)
{
    cout << "The time is = " << setw(2) << setfill('0') << hh << ":"
                             << setw(2) << setfill('0') << mm << ":"
                             << setw(2) << setfill('0') << ss << endl;
    cout << "Time in total seconds: " << seconds;
}
 
int main()
{
    Time T; //creating objects
     
    T.getTime();
    T.convertIntoSeconds();
    T.displayTime();
     
    return 0;
}
-------------



@RestController
@RequestMapping("/api/admin")
@RequiredArgsConstructor
public class BnppShareDebugController {

    private final CalculateBnppShareJob calculateBnppShareJob;

    @PostMapping("/run-bnpp-share-job")
    public ResponseEntity<String> runBnppShareJob() {
        try {
            calculateBnppShareJob.execute(null);  // directly runs job
            return ResponseEntity.ok("BNPP share job executed successfully.");
        } catch (Exception e) {
            return ResponseEntity.internalServerError().body("Error: " + e.getMessage());
        }
    }
}


