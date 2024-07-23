# stream_refectoring

------------------------------------------------------------------------------------------------------------
### 변환 전 코드
```
import org.junit.Test;

@Test
public void beneficiaryProjectUpdate(String projectName, Beneficiary people) {
	for (TalentDonationProject project : donationProjectList) {
		if (project != null && project.getTalentDonationProjectName().equals(projectName)) {
			project.setProjectBeneficiary(people);
   			break;
		}
	}
}
```


### Stream API 변환 후
```
import org.junit.Test;

@Test
public void beneficiaryProjectUpdate(String projectName, Beneficiary people) {
	donationProjectList.stream()
	.filter(project -> project != null && project.getTalentDonationProjectName().equals(projectName))
	.findFirst().ifPresent(project1 -> project1.setProjectBeneficiary(people));
}
```

### 변환 전 코드
```
import org.junit.Test;

@Test
public TalentDonationProject getDonationProject(String projectName) {
		for (TalentDonationProject project : donationProjectList) {
			if (project != null && project.getTalentDonationProjectName().equals(projectName)) {
				return project; //메소드 자체의 종료
			}
		}

		return null;
  }
```

### Stream API 변환 후
```
import org.junit.Test;

@Test
public TalentDonationProject getDonationProject(String projectName) {
		Optional<TalentDonationProject> findproject = donationProjectList.stream()
				.filter(project -> project != null && project.getTalentDonationProjectName()
				.equals(projectName)).findFirst();
		
		return findproject.orElse(null);
}
```
