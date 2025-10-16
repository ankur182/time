it('should open warning popup when sponsors are missing in credit events', (done) => {
  // Arrange
  const matDialogSpy = jest.spyOn(mockMatDialog, 'open');
  component.signatureDate = '2024-06-11';
  component.creditInfoModel = {
    agentName: 'AgentName',
    bnppShare: '12',
  } as any;

  // Mock credit events - no sponsors
  jest
    .spyOn(mockLeverageFacade, 'creditEvents$', 'get')
    .mockReturnValue(of([{ sponsors: [] }]));

  // Act
  component.canExit(true).subscribe((deactivate) => {
    // Assert
    expect(deactivate).toBeFalsy();
    expect(matDialogSpy).toHaveBeenCalledWith(AlertDialogComponent, {
      data: {
        title: 'Warning',
        description:
          '<p>Missing information: Kindly update Sponsors details on credit event.</p>',
        isValidateDisabled: false,
      },
    });
    done();
  });
});
