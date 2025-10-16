async canExit(isLeveragePage: boolean): Promise<boolean> {
  if (!isLeveragePage) return true;

  // 1️⃣ Validate signature date
  if (!this.signatureDate) {
    this.dialog.open<AlertDialogComponent, ConfirmDialogData>(AlertDialogComponent, {
      data: {
        title: 'Warning',
        description: '<p>Missing information: Kindly update closing date on credit information.</p>',
        isValidateDisabled: false,
      },
    });
    return false;
  }

  // 2️⃣ Validate agent name & BNPP share
  if (!this.creditInfoModel?.agentName || !this.creditInfoModel?.bnppShare) {
    this.showWarningInfoDialog();
    return false;
  }

  // 3️⃣ Validate sponsors inside credit events
  const hasSponsors = await firstValueFrom(this.hasSponsorsFromCreditEvents());
  if (!hasSponsors) {
    this.dialog.open<AlertDialogComponent, ConfirmDialogData>(AlertDialogComponent, {
      data: {
        title: 'Warning',
        description: '<p>Missing information: Kindly update Sponsors details on credit event.</p>',
        isValidateDisabled: false,
      },
    });
    return false;
  }

  return true;
}
